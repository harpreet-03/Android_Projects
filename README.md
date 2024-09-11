# My Tip Calculator

## Project Overview
The **My Tip Calculator** is an Android application designed to calculate tips based on the bill amount and the quality of service. Built using **Jetpack Compose**, the app allows users to input the bill amount, tip percentage, and provides an option to round up the tip for convenience.

## Features
- **Bill Amount Input**: Users can enter the total bill amount.
- **Tip Percentage Input**: Users can specify the percentage they want to tip based on the service.
- **Round Up Option**: A toggle switch allows users to round up the calculated tip to the nearest whole number.
- **Responsive UI**: The interface is designed using Jetpack Compose, making it user-friendly and responsive.

## Application Structure
- **MainActivity**: The core activity that launches the UI.
- **Composable Functions**: Modular components used to build the user interface:
  - `TipCalculator()`: The main composable function that builds the UI for tip calculation.
  - `EditNumberField()`: Custom input fields for the bill amount and tip percentage.
  - `RoundTheTipRow()`: A row component with a switch to enable or disable rounding up the tip.

## Code Breakdown

### 1. **MainActivity**
This is the entry point of the application, where the theme is set, and the content is defined.

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyTipTimeTheme {
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = Color(0xFFDDDCD7)
                ) {
                    TipPreview()
                }
            }
        }
    }
}
```
2. Tip Calculator Composable
\n The main UI where users can input the bill amount, tip percentage, and toggle the round-up option. \n

```kotlin
@Composable
fun TipCalculator(modifier: Modifier = Modifier) {
    var tipInput by remember { mutableStateOf("") }
    var amountInput by remember { mutableStateOf("") }
    var roundUp by remember { mutableStateOf(false) }

    val amount = amountInput.toDoubleOrNull() ?: 0.0
    val tipPercent = tipInput.toDoubleOrNull() ?: 0.0
    val tip = calculateTip(amount, tipPercent, roundUp)

    // UI layout with title, input fields, and result display
    Column(verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally,
        modifier = modifier
            .fillMaxSize()
            .padding(horizontal = 40.dp)
            .verticalScroll(rememberScrollState())) {
        ...
    }
}
```

3. Input Fields
Custom composable for input fields with an icon and label.

```kotlin
@Composable
fun EditNumberField(
    value: String,
    @StringRes label: Int,
    @DrawableRes leadingIcon: Int,
    onValueChange: (String) -> Unit,
    keyboardOptions: KeyboardOptions,
    modifier: Modifier = Modifier
) {
    TextField(
        value = value,
        leadingIcon = { Icon(painter = painterResource(id = leadingIcon), null) },
        onValueChange = onValueChange,
        singleLine = true,
        keyboardOptions = keyboardOptions,
        label = { Text(stringResource(label)) }
    )
}

```
4. Rounding Tip Option
A row with a text and switch to enable the rounding feature.

```kotlin

@Composable
fun RoundTheTipRow(
    roundUp: Boolean,
    onRoundUpChanged: (Boolean) -> Unit,
    modifier: Modifier = Modifier
) {
    Row(
        modifier = modifier.fillMaxWidth().size(48.dp),
        verticalAlignment = Alignment.CenterVertically
    ) {
        Text(text = stringResource(R.string.round_up_tip))
        Switch(
            modifier = Modifier.fillMaxWidth().wrapContentWidth(Alignment.End),
            checked = roundUp,
            onCheckedChange = onRoundUpChanged
        )
    }
}
```
5. Tip Calculation Function
A helper function that calculates the tip based on the entered amount and tip percentage.

```kotlin
private fun calculateTip(amount: Double, tipPercent: Double = 15.0, roundUp: Boolean): String {
    var tip = tipPercent / 100 * amount
    if (roundUp) {
        tip = kotlin.math.ceil(tip)
    }
    return NumberFormat.getCurrencyInstance().format(tip)
}

```

6. Preview Function
A preview composable to visualize the app's UI within Android Studio.

```kotlin

@Preview(showBackground = true)
@Composable
fun TipPreview() {
    MyTipTimeTheme {
        TipCalculator()
    }
}

```

##Dependencies
- Jetpack Compose: To build UI components declaratively.
- Material Design 3: For modern UI elements and themes.
- Kotlin: Primary language used in the app development.

##Future Enhancements
- Improving UI
- Add localization support for different currencies.
- Include a dark mode option for the user interface.
- Allow users to save their most common tip percentages.


