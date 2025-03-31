# Golden-Fork-Restaurant

from pynput.mouse import Button, Controller
from pynput.keyboard import Listener, KeyCode
import threading
import time

mouse = Controller()
clicking = False  # Tracks if clicking should continue

def click_loop():
    while True:
        if clicking:
            mouse.click(Button.left)
        time.sleep(0.05)  # Adjust delay for faster/slower clicking


threading.Thread(target=click_loop, daemon=True).start()


def on_press(key):
    global clicking
    if key == KeyCode.from_char('c'):  # Press 'C' to start/stop clicking
        clicking = not clicking


with Listener(on_press=on_press) as listener:
    listener.join()