# Golden-Fork-Restaurant

from pynput.mouse import Button, Controller
from pynput.keyboard import Listener, KeyCode
import threading
import time

mouse = Controller()
clicking = False  # Tracks if clicking should continue

# Function to continuously click while holding the key
def click_loop():
    while True:
        if clicking:
            mouse.click(Button.left)
        time.sleep(0.05)  # Adjust delay for faster/slower clicking

# Start the clicking thread
threading.Thread(target=click_loop, daemon=True).start()

# Function to handle key press
def on_press(key):
    global clicking
    if key == KeyCode.from_char('c'):  # Press 'C' to start/stop clicking
        clicking = not clicking

# Start listening for keyboard input
with Listener(on_press=on_press) as listener:
    listener.join()