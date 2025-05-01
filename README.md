from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters
# Handler cho lệnh /start
def start(update: Update, context) -> None:
    update.message.reply_text('Hello, I am your bot!')
# Handler để xóa tin nhắn dài hơn 250 ký tự
def check_length(update: Update, context) -> None:
    message = update.message
    if message.text and len(message.text) > 250:
        message.delete()
        message.reply_text("Tin nhắn vượt quá 250 ký tự đã bị xóa!")
if __name__ == '__main__':
    # Thay bằng token của bạn
    TOKEN = "7566344843:AAE0mGs1zsy0cIJRpYeSAiWW-4a8sfCrXVM"
    # Tạo Application
    application = Application.builder().token(TOKEN).build()
    # Thêm các handler
    application.add_handler(CommandHandler("start", start))
    application.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, check_length))
    # Chạy bot
    print("Bot is running...")
    application.run_polling()
