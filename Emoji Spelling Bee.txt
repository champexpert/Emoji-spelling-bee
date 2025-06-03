import tkinter as tk
from tkinter import messagebox
import random
import emoji  # <-- import emoji library

# Now use emoji codes instead of raw emojis
emoji_words = [
    {"emoji": ":red_apple:", "word": "apple"},
    {"emoji": ":dog:", "word": "dog"},
    {"emoji": ":car:", "word": "car"},
    {"emoji": ":sun_with_face:", "word": "sun"},
    {"emoji": ":pizza:", "word": "pizza"},
    {"emoji": ":elephant:", "word": "elephant"},
    {"emoji": ":balloon:", "word": "balloon"},
    {"emoji": ":books:", "word": "books"},
    {"emoji": ":musical_note:", "word": "music"},
    {"emoji": ":butterfly:", "word": "butterfly"},
    {"emoji": ":cat:", "word": "cat"},
    {"emoji": ":cloud_with_rain:", "word": "rain"},
    {"emoji": ":rainbow:", "word": "rainbow"},
    {"emoji": ":lion_face:", "word": "lion"},
    {"emoji": ":frog:", "word": "frog"},
    {"emoji": ":fish:", "word": "fish"},
    {"emoji": ":banana:", "word": "banana"},
    {"emoji": ":strawberry:", "word": "strawberry"},
    {"emoji": ":grapes:", "word": "grapes"},
    {"emoji": ":cupcake:", "word": "cupcake"},
    {"emoji": ":doughnut:", "word": "donut"},
    {"emoji": ":hamburger:", "word": "burger"},
    {"emoji": ":french_fries:", "word": "fries"},
    {"emoji": ":carrot:", "word": "carrot"},
    {"emoji": ":ear_of_corn:", "word": "corn"},
    {"emoji": ":cheese_wedge:", "word": "cheese"},
    {"emoji": ":egg:", "word": "egg"},
    {"emoji": ":rocket:", "word": "rocket"},
    {"emoji": ":airplane:", "word": "plane"},
    {"emoji": ":bicycle:", "word": "bicycle"},
    {"emoji": ":bus:", "word": "bus"},
    {"emoji": ":police_car:", "word": "police"},
    {"emoji": ":fire_engine:", "word": "firetruck"},
    {"emoji": ":house:", "word": "house"},
    {"emoji": ":bed:", "word": "bed"},
    {"emoji": ":mobile_phone:", "word": "phone"},
    {"emoji": ":dark_sunglasses:", "word": "sunglasses"},
    {"emoji": ":light_bulb:", "word": "light"},
    {"emoji": ":teddy_bear:", "word": "teddy"},
    {"emoji": ":video_game:", "word": "game"},
]

class EmojiSpellingBee:
    def __init__(self, root):
        self.root = root
        self.root.title("Emoji Spelling Bee")
        self.root.configure(bg="lavender")

        self.score = 0
        self.current_word = ""

        self.emoji_label = tk.Label(root, text="", font=("Segoe UI Emoji", 60), bg="lavender")
        self.emoji_label.pack(pady=20)

        self.entry = tk.Entry(root, font=("Arial", 16))
        self.entry.pack(pady=10)

        self.submit_btn = tk.Button(
            root,
            text="Submit",
            command=self.check_answer,
            font=("Arial", 14),
            bg="#6A5ACD",
            fg="white",
            activebackground="#483D8B",
            padx=15,
            pady=5
        )
        self.submit_btn.pack(pady=10)

        self.feedback = tk.Label(root, text="", font=("Arial", 14), bg="lavender")
        self.feedback.pack()

        self.score_label = tk.Label(root, text="Score: 0", font=("Arial", 12), bg="lavender")
        self.score_label.pack(pady=5)

        self.next_question()

    def next_question(self):
        choice = random.choice(emoji_words)
        self.current_word = choice["word"]
        # Convert emoji code to emoji character
        emoji_char = emoji.emojize(choice["emoji"], language='alias')
        self.emoji_label.config(text=emoji_char)
        self.entry.delete(0, tk.END)
        self.feedback.config(text="")

    def check_answer(self):
        guess = self.entry.get().strip().lower()
        if guess == self.current_word:
            self.score += 1
            self.feedback.config(text="✅ Correct!", fg="green")
        else:
            self.feedback.config(text=f"❌ Oops! It was: {self.current_word}", fg="red")

        self.score_label.config(text=f"Score: {self.score}")
        self.root.after(1500, self.next_question)

if __name__ == "__main__":
    root = tk.Tk()
    app = EmojiSpellingBee(root)
    root.mainloop()
