+++
title = 'Jetpack Compose Navigation Handling of Hilt View Model'
date = 2022-11-04 23:33:47.085000
draft = false
+++
{{< figure src="/images/jetpack-compose-navigation-handling-of-hilt-view-model/Screenshot_from_2022_11_04_23_35_16_f654b730eb.png" alt="hilt-logo" class="center" >}}

Suppose you want to re-use a ViewModel across two full-screen composables, and for some reason you rely on `hiltViewModel()` from `androidx.hilt:hilt-navigation-compose:1.0.0`:

```
@Composable
fun Comp1(viewModel: SharedViewModel = hiltViewModel()) { ... }

@Composable
fun Comp2(viewModel: SharedViewModel = hiltViewModel()) { ... }
```

Let's imagine `Comp1` navigates to `Comp2`.

If you do not pass an explicit handle to existing instance of `SharedViewModel` to these composables, they will go ahead and create a new one for themselves.

The reason for that is the implementation of `hiltViewModel()` internally relies on something called `LocalViewModelStoreOwner` to determine whether it needs to create a new instance or re-use an old one.

The most straightforward solution is of course to just pass a predefined ViewModel instance and not rely on `hiltViewModel()`.

The second approach is to go along with Google and try to supply correct store owners each time you want to re-use something.

Now, the problem with the latter is that it sounds like additional and unnecessary manual work. Before Hilt, in Dagger 2, you had an option to simply mark any object (including a ViewModel) with an appropriate scope or `@Singleton` annotation and just get the correct instance.

You are not allowed to do that on a `@HiltViewModel` now for some reason. Probably it has something to do with these `Context`-tied owners that exist separately from the DI Container.

There arises one question though - why the heck then `hiltViewModel()` and `@HiltViewModel` have `Hilt` in their names? Why we again have to abandon instance-management by Dagger that helped us overcome Activity and Fragment recreations, and start tracking these owners by hand?

Funny thing is, configuration changes do not make `hiltViewModel()` recreate the instances, although the contexts are no longer the same, one would think.

Anyway, kind folks over at StackOverflow shared a better solution [here](https://stackoverflow.com/a/69643625/13442292).