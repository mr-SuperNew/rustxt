---
name: setup
description: Configure rustxt voice profile. Asks for ToV file or creates one through interview.
---

# rustxt setup

Set up voice personalization for the rustxt skill.

## Steps

1. Ask the user: "У тебя есть файл Tone of Voice (описание голоса, стиля письма)? Если да, скинь путь к файлу. Если нет, я помогу создать."

2. **If user has a ToV file:**
   - Read the file to verify it contains voice/style data
   - Ask: "Есть ли файл профиля автора (биография, экспертиза, контекст)? Путь или пропустить."
   - Ask: "Есть ли файл бренд-идентичности? Путь или пропустить."
   - Generate config.md with the provided paths

3. **If user does NOT have a ToV file:**
   - Run a short interview (5-7 questions):
     - "Как бы ты описал свой стиль письма в двух словах? (например: разговорный и прямой, академический, ироничный)"
     - "Какие слова/выражения ты часто используешь?"
     - "Какие слова/выражения тебя бесят в чужих текстах?"
     - "Для кого ты обычно пишешь? (аудитория)"
     - "Покажи 2-3 абзаца текста, который ты написал и которым доволен."
   - Generate a basic ToV file from the answers
   - Save it to the path the user chooses
   - Generate config.md pointing to it

4. **Write config.md** to the skill directory:
   ```
   Glob("**/rustxt/SKILL.md")
   ```
   Use the parent directory of SKILL.md as the target for config.md.

5. Confirm: "Готово. rustxt теперь пишет в твоём голосе. Попробуй: попроси написать или переписать любой текст."
