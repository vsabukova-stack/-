[index.html](https://github.com/user-attachments/files/35432008/index.html)
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Тест и анкета | Модуль согласования ДЗЗ и ADS-B — Скляр В.Ю.</title>
  <style>
    :root {
      --bg-main: #0a0a0f;
      --bg-card: #131324;
      --bg-input: #1b1b33;
      --accent-purple: #7b2fff;
      --accent-cyan: #00d4ff;
      --accent-green: #22c55e;
      --accent-red: #f43f5e;
      --text-main: #f4f6fc;
      --text-muted: #9aa3bd;
      --border: rgba(123, 47, 255, 0.35);
      --radius: 16px;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Inter, Arial, sans-serif;
      background-color: var(--bg-main);
      background-image:
        radial-gradient(circle at 90% 8%, rgba(123, 47, 255, 0.25) 0%, transparent 45%),
        radial-gradient(circle at 10% 90%, rgba(0, 212, 255, 0.18) 0%, transparent 45%);
      color: var(--text-main);
      line-height: 1.5;
      min-height: 100vh;
      padding: 20px 14px 48px;
    }

    .container { max-width: 680px; margin: 0 auto; }

    .hero {
      background: linear-gradient(145deg, rgba(24, 18, 52, 0.95), rgba(16, 16, 32, 0.95));
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 24px 20px;
      margin-bottom: 18px;
      position: relative;
      overflow: hidden;
    }

    .hero::before {
      content: "";
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 4px;
      background: linear-gradient(90deg, var(--accent-purple), var(--accent-cyan));
    }

    .badge {
      display: inline-block;
      font-size: 12px;
      font-weight: 700;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      color: var(--accent-cyan);
      background: rgba(0, 212, 255, 0.12);
      border: 1px solid rgba(0, 212, 255, 0.3);
      padding: 4px 10px;
      border-radius: 999px;
      margin-bottom: 12px;
    }

    h1 { font-size: 22px; line-height: 1.25; margin-bottom: 10px; color: #ffffff; }
    .subtitle { font-size: 14px; color: var(--text-muted); margin-bottom: 14px; }

    .eco-pill {
      display: flex; align-items: center; gap: 8px; font-size: 13px;
      color: #bbf7d0; background: rgba(34, 197, 94, 0.12);
      border: 1px solid rgba(34, 197, 94, 0.3); border-radius: 12px;
      padding: 10px 12px;
    }

    .progress-wrap {
      position: sticky; top: 8px; z-index: 10;
      background: rgba(10, 10, 15, 0.9); backdrop-filter: blur(8px);
      border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 12px;
      padding: 10px 14px; margin-bottom: 16px;
    }

    .progress-meta { display: flex; justify-content: space-between; font-size: 12px; color: var(--text-muted); margin-bottom: 6px; }
    .progress-track { height: 6px; background: rgba(255, 255, 255, 0.08); border-radius: 999px; overflow: hidden; }
    .progress-bar { height: 100%; width: 0%; background: linear-gradient(90deg, var(--accent-purple), var(--accent-cyan)); transition: width 0.25s ease; }

    .section-title {
      font-size: 15px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.06em;
      color: var(--accent-cyan); margin: 22px 0 10px 4px;
    }

    .card {
      background: var(--bg-card); border: 1px solid rgba(123, 47, 255, 0.28);
      border-radius: var(--radius); padding: 18px 16px; margin-bottom: 14px;
    }

    .q-num { font-size: 12px; font-weight: 700; color: #c084fc; text-transform: uppercase; margin-bottom: 6px; }
    .q-text { font-size: 16px; font-weight: 600; color: #ffffff; margin-bottom: 12px; }

    .options { display: flex; flex-direction: column; gap: 8px; }

    .option-label {
      display: flex; align-items: flex-start; gap: 10px;
      background: var(--bg-input); border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 12px; padding: 12px; cursor: pointer; font-size: 14px; color: #e2e8f0;
      transition: border-color 0.2s, background 0.2s; -webkit-tap-highlight-color: transparent;
    }

    .option-label:hover { border-color: var(--accent-cyan); }
    .option-label input[type="radio"] { margin-top: 3px; accent-color: var(--accent-cyan); transform: scale(1.15); flex-shrink: 0; }
    .option-label.selected { border-color: var(--accent-purple); background: rgba(123, 47, 255, 0.18); }
    .option-label.correct { border-color: var(--accent-green); background: rgba(34, 197, 94, 0.18); color: #dcfce7; }
    .option-label.wrong { border-color: var(--accent-red); background: rgba(244, 63, 94, 0.18); color: #ffe4e6; }

    .explanation {
      display: none; margin-top: 10px; padding: 10px 12px; border-radius: 10px; font-size: 13px;
      background: rgba(0, 212, 255, 0.08); border-left: 3px solid var(--accent-cyan); color: #dbeafe;
    }

    .field { margin-bottom: 14px; }
    .field:last-child { margin-bottom: 0; }
    .field label { display: block; font-size: 14px; font-weight: 600; margin-bottom: 6px; color: #e2e8f0; }

    input[type="text"], textarea {
      width: 100%; background: var(--bg-input); border: 1px solid rgba(255, 255, 255, 0.12);
      border-radius: 12px; padding: 12px 14px; color: #ffffff; font-size: 15px;
      font-family: inherit; outline: none;
    }
    input[type="text"]:focus, textarea:focus { border-color: var(--accent-cyan); }
    input[type="text"]:disabled, textarea:disabled { opacity: 0.65; }
    textarea { resize: vertical; min-height: 76px; }

    .rating-row { display: grid; grid-template-columns: repeat(5, 1fr); gap: 8px; }
    .rating-btn {
      background: var(--bg-input); border: 1px solid rgba(255, 255, 255, 0.12); border-radius: 12px;
      padding: 12px 0; color: #ffffff; font-size: 16px; font-weight: 700; cursor: pointer; transition: all 0.2s;
    }
    .rating-btn.active { background: linear-gradient(135deg, var(--accent-purple), #4f46e5); border-color: var(--accent-cyan); box-shadow: 0 0 14px rgba(123, 47, 255, 0.45); }
    .rating-hints { display: flex; justify-content: space-between; font-size: 12px; color: var(--text-muted); margin-top: 6px; }

    .chips { display: flex; flex-wrap: wrap; gap: 8px; }
    .chip {
      background: var(--bg-input); border: 1px solid rgba(255, 255, 255, 0.12); border-radius: 999px;
      padding: 8px 13px; font-size: 13px; color: #e2e8f0; cursor: pointer; transition: all 0.2s;
    }
    .chip.active { background: rgba(0, 212, 255, 0.18); border-color: var(--accent-cyan); color: #ffffff; font-weight: 600; }

    .submit-btn {
      width: 100%; margin-top: 10px; padding: 16px; border: none; border-radius: 14px;
      background: linear-gradient(90deg, var(--accent-purple), #2563eb, var(--accent-cyan));
      color: #ffffff; font-size: 16px; font-weight: 700; cursor: pointer; transition: opacity 0.2s, transform 0.1s;
    }
    .submit-btn:active { transform: scale(0.99); }
    .submit-btn:disabled { opacity: 0.6; cursor: not-allowed; }

    .error-msg {
      display: none; margin-top: 12px; padding: 12px 14px; border-radius: 12px;
      background: rgba(244, 63, 94, 0.15); border: 1px solid var(--accent-red);
      color: #fecdd3; font-size: 14px; text-align: center;
    }

    .result-box {
      display: none; background: linear-gradient(145deg, rgba(24, 18, 52, 0.98), rgba(12, 24, 38, 0.98));
      border: 2px solid var(--accent-cyan); border-radius: 20px; padding: 24px 20px; margin-bottom: 18px; text-align: center;
    }
    .score-big {
      font-size: 46px; font-weight: 800; background: linear-gradient(90deg, #c084fc, var(--accent-cyan));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin: 6px 0;
    }
    .result-verdict { font-size: 17px; font-weight: 600; margin-bottom: 10px; color: #ffffff; }
    .sync-status {
      display: inline-block; font-size: 13px; padding: 6px 12px; border-radius: 999px;
      background: rgba(34, 197, 94, 0.15); color: #86efac; margin-top: 8px;
    }
    .reset-btn {
      margin-top: 14px; background: transparent; border: 1px solid rgba(255, 255, 255, 0.25);
      color: #cbd5e1; padding: 8px 16px; border-radius: 10px; font-size: 13px; cursor: pointer;
    }

    footer { text-align: center; font-size: 12px; color: var(--text-muted); margin-top: 26px; line-height: 1.6; }
  </style>
</head>
<body>
  <div class="container">
    <header class="hero">
      <div class="badge">ГУАП • Кафедра № 24 • Группа 2543</div>
      <h1>Онлайн-тест и анкета по защите курсовой</h1>
      <p class="subtitle">
        Модуль согласования разновременных данных ДЗЗ и ADS-B с оценкой актуальности и достоверности • Скляр В.Ю.
      </p>
      <div class="eco-pill">
        <span>🌿</span>
        <span><strong>Эко-формат:</strong> вместо печати бумажных анкет — лёгкая веб-страница (до 25 КБ), экономия ~125–150 г бумаги на группу.</span>
      </div>
    </header>

    <section id="resultBox" class="result-box" aria-live="polite">
      <div class="badge">Результат проверки</div>
      <div id="scoreText" class="score-big">0 / 6</div>
      <p id="verdictText" class="result-verdict"></p>
      <p class="subtitle" style="margin-bottom: 8px;">
        Ниже под каждым вопросом открылись правильные ответы и короткие пояснения.
      </p>
      <div id="syncStatus" class="sync-status"></div>
      <div>
        <button type="button" class="reset-btn" onclick="location.reload()">Пройти ещё раз</button>
      </div>
    </section>

    <div class="progress-wrap" id="progressWrap">
      <div class="progress-meta">
        <span>Прогресс заполнения</span>
        <span id="progressLabel">0 из 7 обязательных пунктов</span>
      </div>
      <div class="progress-track">
        <div id="progressBar" class="progress-bar"></div>
      </div>
    </div>

    <form id="quizForm" novalidate>
      <div class="section-title">Часть 1. Короткий тест по докладу (6 вопросов)</div>
      <div id="questionsContainer"></div>

      <div class="section-title">Часть 2. Обратная связь для докладчика</div>
      <div class="card">
        <div class="field">
          <label>Насколько понятно была раскрыта тема доклада? *</label>
          <div class="rating-row" id="ratingRow">
            <button type="button" class="rating-btn" data-val="1">1</button>
            <button type="button" class="rating-btn" data-val="2">2</button>
            <button type="button" class="rating-btn" data-val="3">3</button>
            <button type="button" class="rating-btn" data-val="4">4</button>
            <button type="button" class="rating-btn" data-val="5">5</button>
          </div>
          <div class="rating-hints">
            <span>Сложно понять</span>
            <span>Всё супер понятно</span>
          </div>
        </div>

        <div class="field">
          <label>Что запомнилось больше всего?</label>
          <div class="chips" id="topicChips">
            <button type="button" class="chip" data-topic="Смысловая совместимость (ДЗЗ ≠ самолёт)">Смысловая совместимость (ДЗЗ ≠ самолёт)</button>
            <button type="button" class="chip" data-topic="Роль ИИ вне рабочего контура">Роль ИИ вне рабочего контура</button>
            <button type="button" class="chip" data-topic="Испытания Т1–Т8 и повтор Т8">Испытания Т1–Т8</button>
            <button type="button" class="chip" data-topic="Экономика (7 мес. окупаемости)">Экономика и окупаемость</button>
            <button type="button" class="chip" data-topic="Оформление и подача">Оформление и подача</button>
          </div>
        </div>

        <div class="field">
          <label for="respondentName">Имя или фамилия (по желанию — можно анонимно)</label>
          <input type="text" id="respondentName" placeholder="Например: Алексей, гр. 2543" maxlength="80" />
        </div>

        <div class="field">
          <label for="commentField">Вопрос докладчику или комментарий (по желанию)</label>
          <textarea id="commentField" placeholder="Что можно улучшить или о чём хотелось бы узнать подробнее?" maxlength="400"></textarea>
        </div>
      </div>

      <button type="submit" id="submitBtn" class="submit-btn">
        Проверить тест и отправить анкету
      </button>
      <div id="errorMsg" class="error-msg"></div>
    </form>

    <footer>
      Сайт написан на чистом HTML, CSS и JavaScript без тяжёлых фреймворков • ГУАП, 2026<br />
      Сделано для защиты курсовой работы Скляр В.Ю. (руководитель: доц., к.т.н. В.И. Саенко)
    </footer>
  </div>

  <script>
    const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbyIHXQX5GoWy8R0UyKLQeXR-SZhLXVRiFgpGKZwpE4Bs5ZvKfWWo5PAPCBj_j-Mmo0/exec";

    const QUESTIONS = [
      {
        id: "q1",
        text: "Почему данные ДЗЗ (например, спутник Sentinel-2) нельзя считать единственным источником непрерывного наблюдения за самолётами?",
        options: [
          "Спутники не передают географические координаты",
          "Снимки обновляются с большим интервалом (~5–6 дней), а оптика зависит от облачности и освещения",
          "Данные ДЗЗ работают только внутри закрытой локальной сети",
          "Спутники видят только воздушные суда, но не видят поверхность земли"
        ],
        correct: 1,
        explanation: "У Sentinel-2 стандартный цикл повторного наблюдения около 5 дней и мешает облачность, у Sentinel-1 — около 6 дней. Поэтому ДЗЗ дополняют оперативными данными ADS-B."
      },
      {
        id: "q2",
        text: "Какое главное правило смысловой совместимости лежит в основе разработанного модуля?",
        options: [
          "Близкие координаты на карте автоматически означают один и тот же объект",
          "Перед проверкой расстояния проверяется совместимость классов: снимок территории и летящий самолёт не объединяются",
          "При расхождении координат программа усредняет две точки",
          "Несовместимые записи автоматически удаляются без следа"
        ],
        correct: 1,
        explanation: "Центральная идея работы: близость координат ≠ один объект. Снимок аэродрома и сообщение ADS-B о самолёте — разные сущности, их слияние запрещено матрицей совместимости."
      },
      {
        id: "q3",
        text: "Какую роль играют сервисы ИИ (ChatGPT, GigaChat, Поиск с Нейро, DeepSeek) в этом проекте?",
        options: [
          "Они управляют воздушным движением в реальном времени",
          "Они самостоятельно выставляют статус достоверности каждому входящему наблюдению",
          "Они применяются только как инструменты разработчика и не входят в рабочий контур модуля",
          "Они полностью заменяют тестирование и проверку фактов"
        ],
        correct: 2,
        explanation: "Рабочий модуль на Python работает строго по детерминированным правилам из конфигурации, чтобы решения были проверяемыми и воспроизводимыми."
      },
      {
        id: "q4",
        text: "Как модуль оценивает актуальность (возраст) записи наблюдения?",
        options: [
          "По времени загрузки файла на компьютер оператора",
          "По времени события (event_time) относительно момента оценки с раздельными порогами TTL: 120 с для ДЗЗ и 30 с для ADS-B",
          "По единому общему порогу 60 секунд для всех источников",
          "Только по уверенности детектора без учёта времени"
        ],
        correct: 1,
        explanation: "Старый снимок не становится свежим от того, что его загрузили сегодня. Пороги TTL разделены из-за разной природы источников."
      },
      {
        id: "q5",
        text: "Чем результат контрольного теста Т5 (расхождение 557,65 м при пределе 250 м) принципиально отличается от теста Т7 (классы terrain и aircraft)?",
        options: [
          "В Т5 выявляется CONFLICT с сохранением исходных координат, а в Т7 сравнение блокируется раньше — по коду INCOMPATIBLE_CLASS",
          "В обоих тестах программа выдаёт подтверждение CONFIRMED",
          "В Т5 программа останавливается с ошибкой, а в Т7 усредняет координаты",
          "Ничем — в журнале записывается одинаковый код STALE"
        ],
        correct: 0,
        explanation: "Раздельные коды причин в журнале audit.jsonl доказывают, что модуль отличает конфликт координат у допустимого кандидата (Т5) от несовместимости сущностей (Т7)."
      },
      {
        id: "q6",
        text: "Какой расчётный чистый эффект и простой срок окупаемости получены в базовом сценарии (84 комплекта в месяц)?",
        options: [
          "5 000 руб./мес. и окупаемость 24 месяца",
          "16 000 руб./мес. и окупаемость 7 месяцев",
          "45 000 руб./мес. и окупаемость 2 месяца",
          "Внедрение модуля не окупается"
        ],
        correct: 1,
        explanation: "Сокращение времени проверки с 25 до 10 минут освобождает 21 час/мес. (19 950 руб. − 3 950 руб. сопровождения = 16 000 руб./мес.; при затратах 112 000 руб. окупаемость равна 7 мес.)."
      }
    ];

    const state = { answers: {}, rating: null, favoriteTopic: "", submitted: false };
    const container = document.getElementById("questionsContainer");
    const progressBar = document.getElementById("progressBar");
    const progressLabel = document.getElementById("progressLabel");
    const errorMsg = document.getElementById("errorMsg");

    QUESTIONS.forEach((q, idx) => {
      const card = document.createElement("div");
      card.className = "card";
      card.id = "card-" + q.id;
      const optionsHtml = q.options.map((opt, optIdx) => `
        <label class="option-label" data-q="${q.id}" data-opt="${optIdx}">
          <input type="radio" name="${q.id}" value="${optIdx}" />
          <span>${opt}</span>
        </label>
      `).join("");
      card.innerHTML = `
        <div class="q-num">Вопрос ${idx + 1} из ${QUESTIONS.length}</div>
        <div class="q-text">${q.text}</div>
        <div class="options">${optionsHtml}</div>
        <div class="explanation" id="exp-${q.id}">${q.explanation}</div>
      `;
      container.appendChild(card);
    });

    function updateProgress() {
      const answeredCount = Object.keys(state.answers).length + (state.rating ? 1 : 0);
      const totalRequired = QUESTIONS.length + 1;
      const pct = Math.round((answeredCount / totalRequired) * 100);
      progressBar.style.width = pct + "%";
      progressLabel.textContent = `${answeredCount} из ${totalRequired} обязательных пунктов`;
    }

    container.addEventListener("change", (e) => {
      if (state.submitted || e.target.type !== "radio") return;
      const qId = e.target.name;
      const val = Number(e.target.value);
      state.answers[qId] = val;
      document.querySelectorAll(`label[data-q="${qId}"]`).forEach((lbl) => {
        lbl.classList.toggle("selected", Number(lbl.dataset.opt) === val);
      });
      errorMsg.style.display = "none";
      updateProgress();
    });

    document.getElementById("ratingRow").addEventListener("click", (e) => {
      if (state.submitted || !e.target.classList.contains("rating-btn")) return;
      state.rating = Number(e.target.dataset.val);
      document.querySelectorAll(".rating-btn").forEach((btn) => {
        btn.classList.toggle("active", Number(btn.dataset.val) === state.rating);
      });
      errorMsg.style.display = "none";
      updateProgress();
    });

    document.getElementById("topicChips").addEventListener("click", (e) => {
      if (state.submitted || !e.target.classList.contains("chip")) return;
      const topic = e.target.dataset.topic;
      state.favoriteTopic = state.favoriteTopic === topic ? "" : topic;
      document.querySelectorAll(".chip").forEach((ch) => {
        ch.classList.toggle("active", ch.dataset.topic === state.favoriteTopic);
      });
    });

    document.getElementById("quizForm").addEventListener("submit", async (e) => {
      e.preventDefault();
      if (state.submitted) return;

      if (Object.keys(state.answers).length < QUESTIONS.length) {
        errorMsg.textContent = "Пожалуйста, ответь на все 6 вопросов теста перед отправкой.";
        errorMsg.style.display = "block";
        return;
      }
      if (!state.rating) {
        errorMsg.textContent = "Поставь, пожалуйста, оценку понятности доклада от 1 до 5.";
        errorMsg.style.display = "block";
        return;
      }

      state.submitted = true;
      const submitBtn = document.getElementById("submitBtn");
      const nameInput = document.getElementById("respondentName");
      const commentInput = document.getElementById("commentField");
      submitBtn.disabled = true;
      nameInput.disabled = true;
      commentInput.disabled = true;
      submitBtn.textContent = "Проверяем ответы...";

      let score = 0;
      QUESTIONS.forEach((q) => {
        const userChoice = state.answers[q.id];
        if (userChoice === q.correct) score++;
        document.querySelectorAll(`label[data-q="${q.id}"]`).forEach((lbl) => {
          const optIdx = Number(lbl.dataset.opt);
          lbl.classList.remove("selected");
          if (optIdx === q.correct) lbl.classList.add("correct");
          if (optIdx === userChoice && userChoice !== q.correct) lbl.classList.add("wrong");
          lbl.querySelector("input").disabled = true;
        });
        document.getElementById("exp-" + q.id).style.display = "block";
      });

      let verdict = "Отличный результат! Суть работы и логика модуля усвоены на 100%.";
      if (score <= 2) {
        verdict = "Спасибо за участие! Пояснения ниже помогут быстро освежить ключевые идеи проекта.";
      } else if (score <= 4) {
        verdict = "Хороший результат! Главные принципы согласования ДЗЗ и ADS-B схвачены верно.";
      }

      document.getElementById("scoreText").textContent = `${score} / ${QUESTIONS.length}`;
      document.getElementById("verdictText").textContent = verdict;
      document.getElementById("resultBox").style.display = "block";
      document.getElementById("progressWrap").style.display = "none";
      submitBtn.textContent = "Анкета завершена ✓";

      const syncStatus = document.getElementById("syncStatus");
      const payload = {
        timestamp: new Date().toISOString(),
        name: (nameInput.value || "Аноним").trim(),
        score: score,
        total: QUESTIONS.length,
        rating: state.rating,
        favorite_topic: state.favoriteTopic || "Не выбрано",
        comment: (commentInput.value || "").trim(),
        answers: QUESTIONS.map((q) => `${q.id}:${state.answers[q.id] === q.correct ? "OK" : "ERR"}`).join(", ")
      };

      if (SCRIPT_URL && SCRIPT_URL.startsWith("https://")) {
        syncStatus.textContent = "Сохраняем ответ в таблицу...";
        try {
          const res = await fetch(SCRIPT_URL, {
            method: "POST",
            redirect: "follow",
            headers: { "Content-Type": "text/plain;charset=utf-8" },
            body: JSON.stringify(payload)
          });
          if (res.ok) {
            syncStatus.textContent = "Ответ записан в таблицу докладчика ✓";
            syncStatus.style.color = "#86efac";
          } else {
            syncStatus.textContent = "Тест проверен локально (сервер таблицы временно недоступен)";
            syncStatus.style.color = "#fecdd3";
          }
        } catch (err) {
          syncStatus.textContent = "Тест проверен локально (нет связи с таблицей)";
          syncStatus.style.color = "#fecdd3";
        }
      } else {
        syncStatus.textContent = "Результат рассчитан мгновенно в браузере ✓";
      }

      window.scrollTo({ top: 0, behavior: "smooth" });
    });
  </script>
</body>
</html>
