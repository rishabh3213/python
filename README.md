imimport random
port ipywidgets as widgets
from IPython.display import display

# Generate random number
secret_number = random.randint(1, 100)
attempts = 0

title = widgets.HTML("<h2>🎮 Number Guessing Game</h2>")
instructions = widgets.HTML("<b>Guess a number between 1 and 100</b>")

guess_box = widgets.IntText(
    value=1,
    description='Guess:',
    style={'description_width': 'initial'}
)

submit_btn = widgets.Button(
    description="Submit",
    button_style="success",
    icon="check"
)

restart_btn = widgets.Button(
    description="Restart",
    button_style="warning",
    icon="refresh"
)

output = widgets.Output()

def submit_clicked(b):
    global secret_number, attempts

    guess = guess_box.value
    attempts += 1

    with output:
        output.clear_output()

        if guess < secret_number:
            print("📉 Too Low!")
        elif guess > secret_number:
            print("📈 Too High!")
        else:
            print(f"🎉 Congratulations!")
            print(f"You guessed the number in {attempts} attempts.")

            submit_btn.disabled = True

def restart_clicked(b):
    global secret_number, attempts

    secret_number = random.randint(1, 100)
    attempts = 0

    submit_btn.disabled = False
    guess_box.value = 1

    with output:
        output.clear_output()
        print("🔄 New Game Started!")

submit_btn.on_click(submit_clicked)
restart_btn.on_click(restart_clicked)

display(title)
display(instructions)
display(guess_box)
display(widgets.HBox([submit_btn, restart_btn]))
display(output)

