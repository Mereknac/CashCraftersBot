# CashCraftersBot
 
import telebot
import requests

# Bot-Token einfügen
bot = telebot.TeleBot("6708100945:AAFMbcih7QeOQTd4d6MImrnBMV-3ApUHQ_k")

# Telegram-Gruppenlink und Benutzernamen
group_link = "https://t.me/FalsGeldpremium"
username = "@CashCraftersBot"

# Funktion für ChatGPT-Anfrage
def get_chatgpt_response(message):
    # Hier die URL deines ChatGPT-Servers einfügen
    url = "URL_DEINES_CHATGPT_SERVERS_HIER"
    payload = {"message": message}
    response = requests.post(url, json=payload)
    return response.json()["response"]

# Bot-Befehle definieren
@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.reply_to(message, f"Hallo! Ich bin {username}.\n"
                          f"Du kannst mich in meiner Telegramm-Gruppe finden: {group_link}\n"
                          "Um Falschgeld zu bestellen, verwende /bestellen.\n"
                          "Um Hilfe zu erhalten, verwende /hilfe.")

@bot.message_handler(commands=['hilfe'])
def send_help(message):
    bot.reply_to(message, "Wie kann ich Ihnen helfen?\n"
                          "Um Falschgeld zu bestellen, verwenden Sie /bestellen.\n"
                          "Für weitere Informationen und Optionen, besuchen Sie unsere Telegramm-Gruppe.")

@bot.message_handler(commands=['bestellen'])
def order_fake_money(message):
    bot.reply_to(message, "Hier sind unsere aktuellen Preise für Falschgeld:\n"
                          "- 100€ Schein für nur 30€\n"
                          "- 200€ Schein für nur 50€\n"
                          "- 500€ Schein für nur 100€\n"
                          "Bitte beachten Sie, dass bei höheren Nachfragen die Preise variieren können.\n"
                          "Für die Versandbeschreibung und Zahlungsmöglichkeiten kontaktieren Sie uns bitte direkt.")

@bot.message_handler(func=lambda message: True)
def echo_all(message):
    if "versand" in message.text.lower():
        bot.reply_to(message, "Bestellungen werden sicher und unauffällig verpackt, damit Sie sich keine Sorgen machen müssen.")
    elif "zahlungsmöglichkeiten" in message.text.lower():
        bot.reply_to(message, "Als Zahlungsmöglichkeiten akzeptieren wir PayPal Guthaben und iTunes Karten für Ihre Bequemlichkeit.\n"
                              "Bei iTunes Karten ab 100€ wird zunächst die Hälfte des Guthabens überprüft, bevor der zweite Code verlangt wird.")
    else:
        # Send message to ChatGPT for response
        response = get_chatgpt_response(message.text)
        bot.reply_to(message, response)

# Bot starten
bot.polling()

