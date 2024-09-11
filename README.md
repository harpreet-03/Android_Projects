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
