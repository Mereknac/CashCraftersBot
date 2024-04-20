# CashCraftersBot
 

import telebot

# Bot-Token einfügen
bot = telebot.TeleBot("6708100945:AAFMbcih7QeOQTd4d6MImrnBMV-3ApUHQ_k")

# Bot-Befehle definieren
@bot.message_handler(commands=['start', 'help'])
def send_welcome(message):
    bot.reply_to(message, "Hallo! Ich bin der @CashCraftersBot. Wie kann ich dir helfen?")

# Bot starten
bot.polling()
