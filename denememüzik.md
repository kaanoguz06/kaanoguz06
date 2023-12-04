import telegram
from telegram.ext import Updater, CommandHandler
import subprocess
import threading

TOKEN = '6864389335:AAEn8sdItS2aXSFxvTeUNLi8Nh1V9Z993Aw'


[RADYO_YAYIN_LINKI](http://yayin.radyoseymen.com.tr:1070/;stream.mp3) = ['RADYO_YAYIN_LINKI'](http://yayin.radyoseymen.com.tr:1070/;stream.mp3)


# Botun durumunu takip eden değişken
active = False

# /start komutu için işlev
def start(update, context):
    user_id = update.message.from_user.id
    context.bot.send_message(chat_id=user_id, text="Merhaba! Ben müzik botu. .Galaxyfm komutu ile müzik yayınına başlayabilirsin.")

# /hey komutu için işlev
def hey(update, context):
    global active
    user_id = update.message.from_user.id

    if not active:
        context.bot.send_message(chat_id=user_id, text="Müzik yayını başlıyor...")
        threading.Thread(target=start_radio).start()
        active = True
    else:
        context.bot.send_message(chat_id=user_id, text="Müzik yayını zaten aktif.")

# Radyo yayını işlemini başlatan işlev
def start_radio():
    global active
    subprocess.call(['mpv', http://yayin.radyoseymen.com.tr:1070/;stream.mp3])
    active = False

# Ana işlev
def main():
    updater = Updater(token=TOKEN, use_context=True)
    dispatcher = updater.dispatcher

    # Komut işlevleri
    dispatcher.add_handler(CommandHandler("start", start))
    dispatcher.add_handler(CommandHandler("hey", hey))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
