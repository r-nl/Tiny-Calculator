<script lang="ts">
    // A very simple calculator app built in tailwind/svelte to play with deployment practice.
    import CalculatorButton from "./calculatorButton.svelte";
    let displayText: string[] = [""];
    let answerText: string;
    let answered: boolean = false;

    function calculateAnswer(displayText: string[]) {
        answered = true;
        const sanitizedString = displayText.join().replace(/[^-()\d/*+.]/g, "");
        // Eval is dangerious on server side. That said, this is client side so they can run whatever they want
        // +0 on each side stabilizes illegal bare operations and legalizes some "obvious" expressions like "1+1-".
        answerText = eval("0+" + sanitizedString + "+0") as string;
    }

    function handleButtonPress(event: CustomEvent): void {
        const buttonPressed = event.detail.button;
        if (typeof buttonPressed == "number") {
            displayText.push(buttonPressed.toString());
            displayText = displayText;
        } else {
            if (buttonPressed == "+" || buttonPressed == "-") {
                displayText.push(" " + buttonPressed + " ");
                displayText = displayText;
            } else if (buttonPressed == "=") {
                calculateAnswer(displayText);
            } else {
                displayText = [""];
                answered = false;
            }
        }
    }
</script>

<div
    class="w-full h-screen bg-slate-700 text-slate-50 flex items-center flex-col justify-center font-sans"
>
    <div class="text-2xl font-semibold hidden sm:block">This is a...</div>
    <div class="bg-slate-500 sm:rounded-xl p-5 shadow-lg sm:my-10 h-full w-full sm:w-fit sm:h-fit">
        <div class="flex w-full">
            <div class="bg-slate-950 p-3 rounded-xl w-full mr-3">
                {answered ? answerText : displayText?.join("")}
            </div>
            <CalculatorButton
                buttonLabel="C"
                on:buttonPressed={handleButtonPress}
            />
        </div>
        <div class="h-[80%] sm:h-fit p-5 sm:py-4 sm:p-0 grid grid-cols-4 gap-3">
            <CalculatorButton
                buttonLabel={1}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={2}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={3}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel="+"
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={4}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={5}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={6}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel="-"
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={7}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={8}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel={9}
                on:buttonPressed={handleButtonPress}
            />
            <CalculatorButton
                buttonLabel="="
                on:buttonPressed={handleButtonPress}
            />
        </div>
    </div>
    <div class="text-4xl font-bold hidden sm:block">CALCULATOR!</div>
</div>
