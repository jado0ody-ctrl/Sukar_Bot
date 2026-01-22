import telebot

from telebot import types

import random



# 

TOKEN = '8517951966:AAGkNLBKRDoih7fKNeuaRCxPgm28vlxP5Qo'

bot = telebot.TeleBot(TOKEN)



# 1. رسالة الترحيب الشيك (بدون اسم)

@bot.message_handler(commands=['start'])

def start(message):

    welcome_text = (

        "✨ **أهلاً بك في عالم سُكر الذكي** ✨\n\n"

        "أنا مساعدك المطور للحماية والترفيه 🍬\n\n"

        "🛡 **المالك الرسمي:** @JoudyMedhat\n"

        "------------------------------\n"

        "🎮 اكتب 'العاب' لبدء الاستمتاع!"

    )

    markup = types.InlineKeyboardMarkup()

    markup.add(types.InlineKeyboardButton("👑 تواصل مع المطور", url="https://t.me/JoudyMedhat"))

    bot.send_message(message.chat.id, welcome_text, reply_markup=markup, parse_mode='Markdown')



# 2. الردود الذكية ومنيو الألعاب

@bot.message_handler(func=lambda m: True)

def handle_all(message):

    text = message.text

    

    # ردود سكر

    if text in ['سكر', 'سُكر']:

        bot.reply_to(message, random.choice(['عيوني', 'خير', 'شنو', 'شتريد', 'نعم ياعسل 😉']))

    

    # الردود الكوميدية

    elif 'زق' in text:

        bot.reply_to(message, "مافي زق غيرك 🗿")

    elif 'خرا' in text or 'خرء' in text:

        bot.reply_to(message, "يعني اكلك؟")



    # منيو الألعاب

    elif text == 'العاب':

        markup = types.ReplyKeyboardMarkup(resize_keyboard=True)

        markup.add('لعبة الازياء', 'لعبة المطعم')

        bot.send_message(message.chat.id, "اختار اللعبة يا سكر: 🎮", reply_markup=markup)



    # لعبة الازياء

    elif text == 'لعبة الازياء':

        msg = ("«☆ يرجى ارسال الصورة واسم عارض الازياء للخاص لكي يتم اضافتك لعرض الازياء.»\n"

               "الملصقات ☜ \nhttps://t.me/addstickers/eh7u8djji7dj8")

        bot.send_message(message.chat.id, msg)



print("كود سُكر جاهز..")

bot.infinity_polling()