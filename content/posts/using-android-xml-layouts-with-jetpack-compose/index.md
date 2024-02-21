+++
title = 'Using Android Xml Layouts With Jetpack Compose'
date = 2022-11-03 16:51:39.276000
draft = false
+++

{{< figure src="./images/Screenshot_from_2022_11_03_16_50_26_9e06e66dfc.png" alt="heroes-logo" class="center" >}}

The documentation suggests to use AndroidViewBinding API for the task.

I intended to learn Compose in my project, but also wanted a LineChart from MPAndroidChart library.

Here is what I did. In the fragment:

```kotlin
    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val lineChart = FragmentChartBinding.inflate(inflater)
        return ComposeView(requireContext()).apply {
            setContent {
                SetContent(viewModel, findNavController(), lineChart)
            }
        }
    }
```

And in the composable:

```kotlin
@Composable
fun setChart(
    state: State<List<BodyMeasurement.OxygenMeasurement>>,
    lineChart: FragmentChartBinding
) = AndroidViewBinding(
    bindingBlock = { _, _, _ ->
        lineChart
    },
    modifier = Modifier
        .fillMaxSize(),
    update = { refreshChartData(lineChart, state.value) }
)
```

The samples that I found on the internet dealt with static views, so I wrote this little note. Enjoy!

The quoted code is at [GitHub](https://github.com/pratclot/oxygentracker/blob/7cb153ca429818917f432c6a0a6ba9987a68618e/app/src/main/java/com/pratclot/oxygentracker/fragments/FragmentChart.kt).