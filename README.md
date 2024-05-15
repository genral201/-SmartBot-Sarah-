import pyttsx3
import speech_recognition as sr
import webbrowser
import time
import datetime
import os
from pydub import AudioSegment
from pydub.playback import play
import tkinter as tk
import requests

# تعريف فئة SmartBot
class SmartBot:
    def __init__(self):
        self._products = []
        self._interactions = []
        self._locations = []
        self.engine = pyttsx3.init('arabic')
        self.recognizer = sr.Recognizer()

    def add_product(self, id, name, price):
        product = Product(id, name, price)
        self._products.append(product)

    def display_products(self):
        for product in self._products:
            print(f"الرقم: {product.id}، الاسم: {product.name}، السعر: {product.price}")

    def get_all_products(self):
        return self._products

    def optimize_algorithms(self):
        # تنفيذ تحسين الخوارزميات هنا
        pass

    def interact_with_user(self, interaction_type, details):
        interaction = UserInteraction(interaction_type, details)
        self._interactions.append(interaction)

    def display_interactions(self):
        for interaction in self._interactions:
            print(f"النوع: {interaction.interaction_type}، التفاصيل: {interaction.details}")

    def add_location(self, name, address):
        location = Location(name, address)
        self._locations.append(location)

    def display_locations(self):
        for location in self._locations:
            print(f"الاسم: {location.name}، العنوان: {location.address}")

    def analyze_data(self):
        # تنفيذ تحليل البيانات باستخدام التعلم الآلي هنا
        pass

    def improve_user_interaction(self):
        # إنشاء واجهة مستخدم رسومية لتحسين التفاعل
        root = tk.Tk()
        label = tk.Label(root, text="مرحبًا، مستخدم!")
        label.pack()
        root.mainloop()

    def integrate_apis(self):
        # مثال على دمج APIs باستخدام مكتبة requests
        response = requests.get('https://api.example.com/data')
        data = response.json()
        print(data)

    def play_music(self, file_path):
        # استخدام مكتبة pydub لتشغيل ملفات الصوت مع تحسين الصوت
        song = AudioSegment.from_file(file_path, format="mp3")
        enhanced_song = song + 6  # زيادة مستوى الصوت بمقدار 6 ديسيبل
        play(enhanced_song)

    def speak(self, text):
        self.engine.say(text)
        self.engine.runAndWait()

    def listen(self):
        with sr.Microphone() as mic:
            print("جارٍ الاستماع... تحدث:")
            audio = self.recognizer.listen(mic)
            try:
                query = self.recognizer.recognize_google(audio, language="ar-AR")
                print(f"قلت: {query}")
                return query.lower()
            except sr.UnknownValueError:
                print("عذرًا، لم أفهم ما قلته.")
                return None

    def open_website(self, url):
        webbrowser.open(url)

    def get_time(self):
        current_time = datetime.datetime.now().strftime("%I:%M %p")
        self.speak(f"الوقت الحالي هو {current_time}")

    def get_date(self):
        today = datetime.date.today().strftime("%d/%m/%Y")
        self.speak(f"التاريخ اليوم هو {today}")

    def play_music_file(self, file_path):
        if os.path.isfile(file_path):
            self.play_music(file_path)
        else:
            self.speak(f"عذرًا، الملف {file_path} غير موجود.")

# تعريف فئة المنتج
class Product:
    def __init__(self, id, name, price):
        self.id = id
        self.name = name
        self.price = price

# تعريف فئة التفاعل مع المستخدم
class UserInteraction:
    def __init__(self, interaction_type, details):
        self.interaction_type = interaction_type
        self.details = details

# تعريف فئة الموقع
class Location:
    def __init__(self, name, address):
        self.name = name
        self.address = address

# الاستخدام
if __name__ == "__main__":
    sarah = SmartBot()

    sarah.add_product(1, "منتج 1", 99.99)
    sarah.add_product(2, "منتج 2", 199.99)

    sarah.display_products()

    sarah.interact_with_user("استفسار", "كيف يمكنني شراء منتج؟")

    sarah.display_interactions()

    # إضافة المزيد من الوظائف حسب الحاجة
    while True:
        command = sarah.listen()
        if command:
            if "افتح" in command:
                url = command.split(" ")[1]
                sarah.open_website(url)
            elif "الوقت" in command:
                sarah.get_time()
            elif "التاريخ" in command:
                sarah.get_date()
            elif "شغل موسيقى" in command:
                file_path = command.split(" ")[2]
                sarah.play_music_file(file_path)
            elif "اخرج" in command:
                break
            else:
                sarah.speak("عذرًا، لم أفهم هذا الأمر.")
