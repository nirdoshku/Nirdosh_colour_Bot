# Nirdosh_colour_Bot
import logging
from aiogram import Bot, Dispatcher, types, executor

API_TOKEN = '7982397493:AAG0R_bQhcAM5jr0iQqerBlD1tObqLjGIRQ'  # Replace with your token if needed

logging.basicConfig(level=logging.INFO)
bot = Bot(token=API_TOKEN)
dp = Dispatcher(bot)

# 🔮 Simple prediction logic (placeholder – customize as needed)
def predict_color(number: str):
    num = int(number[-1])
    color = "RED" if num % 3 == 0 else "GREEN" if num % 2 == 0 else "VIOLET"
    size = "BIG" if num >= 5 else "SMALL"
    return f"🎯 Prediction:\nColor: {color}\nNumber: {num}\nSize: {size}"

@dp.message_handler(commands=['start'])
async def start(message: types.Message):
    await message.reply("👋 Welcome to Tiranga Smart Prediction Bot!\nUse /smart 1234 to get prediction.")

@dp.message_handler(commands=['smart'])
async def smart_predict(message: types.Message):
    try:
        input_number = message.text.split(" ")[1]
        if not input_number.isdigit() or len(input_number) != 4:
            raise ValueError
        prediction = predict_color(input_number)
        await message.reply(prediction)
    except:
        await message.reply("❗ Format error! Use like: /smart 1234")

if __name__ == '__main__':
    executor.start_polling(dp, skip_updates=True) 
