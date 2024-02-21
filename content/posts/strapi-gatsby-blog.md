+++
title = 'Strapi Gatsby Blog'
date = 2022-11-02 13:13:31.319000
+++


{{< figure src="/images/strapi-gatsby-blog/Screenshot_from_2022_11_02_13_14_20_31889ed3e1.png" alt="strapi site picture" class="center" >}}

Here is the path I took to host my personal site with Strapi + Gatsby setup.

I had only one previous experience hosting a personal website, that was self hosting with [Ghost](https://ghost.org/) platform version 3. It was a good one with a very intuitive article creation and editing process.

I decided to try something else, and then learned there are headless CMS solutions which *may* work with any static site generator. Compared to Ghost, that would require me to manage 2 systems, plus figure out how to integrate them. I spent a day learning about existing offers ([this](https://jamstack.org/headless-cms/) place is helpful), tried a few and quickly realized that the integration step is the main challenge in a split system approach.

At some point I was able to run a starter from Strapi that was already integrated with Gatsby:

```bash
yarn create strapi-starter my-project gatsby-blog
```
[Here](https://strapi.io/blog/build-a-static-blog-with-gatsby-and-strapi) is a nice blog post about it also.

Then I made a docker container to deploy Gastby, you can find it [here](https://github.com/pratclot/pratclot.com).

The Strapi part required a bit of configuration before it was usable.

The uploads are stored in a directory local to backend code by default. These files are not going to survive if you decide to run the admin panel in a docker container. Placing them in a docker volume is the next reasonable thought, but it adds complexity to the setup. The ghost platform I used before used the database as a single source of truth by default.

I tried to integrate `strapi-provider-mysql-files`  found [here](https://gitlab.com/themineraria/strapi_mysql_files), as there is no official plugin / provider. The provider integration worked as written in README, however, at the time of writing, the code for the plugin was written for Strapi version 3, so I needed to adapt it to version 4. You basically need to generate a new plugin with this:

```bash
yarn strapi generate
```

And then add the code from Cyprien's plugin to a middleware (or a controller, or elsewhere), enriched the plugin's config with SQL server parameters (as in v4 it seems you cannot access other plugin's configs), enable that middleware in `config/middlewares.js` (again, you probably can automate this by utilizing v4's plugin lifecycle API) and it should work.

After this I decided to use S3 instead. There is official support for it by Strapi, and they [have](https://strapi.io/blog/how-to-set-up-amazon-s3-upload-provider-plugin-for-our-strapi-app) a nice blog post about it.

There is one additional step to make the thumbnails work in the admin panel in this setup. The bucket has to have a certain CORS policy configured:

```
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET"],
    "AllowedOrigins": ["YOUR STRAPI URL"],
    "ExposeHeaders": [],
    "MaxAgeSeconds": 3000
  }
]
```

It is taken from [here](https://github.com/strapi/strapi/tree/main/packages/providers/upload-aws-s3). `AllowedOrigins` in my case looks like this:

```
["pratclot.com",  "localhost:1337"]
```

In case you need to further develop the project, you may want to enable GraphQL playground. For v4 there is a solution [here](https://stackoverflow.com/a/73626902/13442292), it will look like this:

```
// path: ./config/plugins.js

module.exports = {
  //
  graphql: {
    config: {
      endpoint: '/graphql',
      shadowCRUD: true,
      playgroundAlways: true, <----- this one
      depthLimit: 7,
      amountLimit: 100,
      apolloServer: {
        tracing: false,
        introspection: true, <----- also this for production deployment
      },
    },
  },
};

```

Now, the content-types that represent the pages of the site are stored on disk, and there is no way to keep them together with other configurations in the database. This seems like a major turn-down that is not advertised.

Finally, the deployment. Strapi and Gatsby are located on different machines, so to deploy the site I run this improvisational script:

```bash
#!/bin/sh

set -e

yarn docker:frontend
docker save pratclot.com.frontend -o pratclot.com.frontend.tar
rsync -avz pratclot.com.frontend.tar myvps:~/
ssh myvps << EOF
    sudo docker load -i pratclot.com.frontend.tar &&
    sudo docker-compose -f \$(find . -type d -name pratclot.com)/docker-compose.centos.yml down &&
    sudo docker-compose -f \$(find . -type d -name pratclot.com)/docker-compose.centos.yml up -d &&
    curl https://pratclot.com --fail -I
EOF
```

Basically, the above explains that I am too poor to have a container registry and k8s, so I transfer and run the container by hand :)