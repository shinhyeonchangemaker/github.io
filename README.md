<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<style>
:root{padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
body{margin:0}
img{max-width:100%}
[hidden]{display:none!important}
</style>
<title>이거 어디 버려?</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Noto+Sans+KR:wght@400;500;700&display=swap">
<style>
/* Layout: phone-first bin-sticker page — search on top, one colored "bin label" card per 수거함, quiz reveals below */
:root {
  --bg: #F1F5F2;
  --surface: #FFFFFF;
  --ink: #17211C;
  --muted: #56655D;
  --line: #D3DDD7;
  --accent: #1E7149;
  --accent-ink: #FFFFFF;
  --plastic: #2C68AB;
  --can: #5E6873;
  --paper: #9A6631;
  --general: #33393F;
  --bin-ink: #FFFFFF;
  --ok-bg: #E4F1E9;
  --no-bg: #F6E7E5;
  --no-ink: #9C3A2E;
  --focus: #1E7149;
  --display: "Black Han Sans", "Noto Sans KR", "Apple SD Gothic Neo", "Malgun Gothic", sans-serif;
  --body: "Noto Sans KR", "Apple SD Gothic Neo", "Malgun Gothic", system-ui, sans-serif;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #111814; --surface: #1A231E; --ink: #E6EEE9; --muted: #9FB0A6; --line: #2E3A33;
    --accent: #5CC28E; --accent-ink: #0E1A13;
    --plastic: #4C86C8; --can: #7D8792; --paper: #B98447; --general: #4A5259; --bin-ink: #FFFFFF;
    --ok-bg: #1D3327; --no-bg: #3A2320; --no-ink: #F0A396; --focus: #5CC28E;
    color-scheme: dark;
  }
}
:root[data-theme="dark"] {
  --bg: #111814; --surface: #1A231E; --ink: #E6EEE9; --muted: #9FB0A6; --line: #2E3A33;
  --accent: #5CC28E; --accent-ink: #0E1A13;
  --plastic: #4C86C8; --can: #7D8792; --paper: #B98447; --general: #4A5259; --bin-ink: #FFFFFF;
  --ok-bg: #1D3327; --no-bg: #3A2320; --no-ink: #F0A396; --focus: #5CC28E;
  color-scheme: dark;
}

* { box-sizing: border-box; }
html { -webkit-text-size-adjust: 100%; text-size-adjust: 100%; }
body {
  background: var(--bg);
  color: var(--ink);
  font-family: var(--body);
  font-size: 16px;
  line-height: 1.6;
  word-break: keep-all;
  overflow-wrap: anywhere;
}
.wrap {
  max-width: 760px;
  margin: 0 auto;
  padding-block: 28px 40px;
  padding-left: max(16px, env(safe-area-inset-left, 0px));
  padding-right: max(16px, env(safe-area-inset-right, 0px));
  display: flex;
  flex-direction: column;
  gap: 28px;
}

/* Header */
.eyebrow {
  font-size: 13px; font-weight: 700; letter-spacing: 0.06em;
  color: var(--accent); margin: 0 0 6px;
}
h1 {
  font-family: var(--display); font-weight: 400;
  font-size: clamp(40px, 11vw, 64px); line-height: 1.05;
  margin: 0; text-wrap: balance;
}
.lede { margin: 10px 0 0; color: var(--muted); max-width: 34em; }

/* "You are here" banner from bin QR */
.here {
  display: flex; align-items: center; gap: 12px;
  padding: 12px 14px; border-radius: 10px;
  background: var(--here-color, var(--accent)); color: var(--bin-ink);
  font-weight: 700;
}
.here { justify-content: space-between; flex-wrap: wrap; }
.here small { display: block; font-weight: 400; opacity: 0.9; }
.here-btn {
  font: inherit; font-size: 14px; font-weight: 700; cursor: pointer; white-space: nowrap;
  padding: 8px 12px; border-radius: 8px; border: 1px solid currentColor;
  background: transparent; color: var(--bin-ink);
}
.here-btn:focus-visible { outline: 2px solid var(--bin-ink); outline-offset: 2px; }

/* Search */
.search label { display: block; font-weight: 700; margin-bottom: 8px; }
.search input {
  width: 100%; font: inherit; font-size: 17px;
  padding: 14px 16px; border-radius: 10px;
  border: 2px solid var(--line); background: var(--surface); color: var(--ink);
}
.search input:focus-visible { outline: none; border-color: var(--focus); }
.chips { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 10px; }
.chip {
  font: inherit; font-size: 14px; padding: 6px 12px; border-radius: 999px;
  border: 1px solid var(--line); background: var(--surface); color: var(--ink); cursor: pointer;
}
.chip:hover { border-color: var(--accent); }
.chip:focus-visible { outline: 2px solid var(--focus); outline-offset: 2px; }
.results { display: flex; flex-direction: column; gap: 8px; margin-top: 14px; }
.result {
  display: grid; grid-template-columns: auto 1fr; gap: 4px 12px; align-items: center;
  padding: 12px 14px; border-radius: 10px; background: var(--surface); border: 1px solid var(--line);
}
.result .tag {
  grid-row: span 2; font-family: var(--display); font-size: 15px; color: var(--bin-ink);
  padding: 8px 10px; border-radius: 8px; min-width: 76px; text-align: center; line-height: 1.2;
}
.result strong { font-size: 16px; }
.result span { color: var(--muted); font-size: 14px; }
.empty { color: var(--muted); font-size: 15px; margin: 4px 0 0; }
.ai-link {
  display: inline-block; margin-top: 14px; font-weight: 700; color: var(--accent);
  padding: 10px 14px; border-radius: 10px; border: 2px solid var(--accent); text-decoration: none;
}
.ai-link:focus-visible { outline: 2px solid var(--focus); outline-offset: 2px; }

/* Bin cards */
h2 { font-family: var(--display); font-weight: 400; font-size: 28px; margin: 0 0 12px; text-wrap: balance; }
.bins { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 14px; }
@media (max-width: 620px) { .bins { grid-template-columns: 1fr; } }
.bin {
  background: var(--surface); border: 1px solid var(--line); border-radius: 12px;
  min-width: 0; scroll-margin-top: 16px; transition: box-shadow 0.2s ease;
}
.bin.is-here { box-shadow: 0 0 0 3px var(--bin-color); }
.bin header {
  background: var(--bin-color); color: var(--bin-ink); border-radius: 11px 11px 0 0;
  padding: 12px 16px; display: flex; align-items: baseline; justify-content: space-between; gap: 10px;
}
.bin header h3 { font-family: var(--display); font-weight: 400; font-size: 24px; margin: 0; }
.bin header span { font-size: 13px; opacity: 0.9; }
/* 상자 안은 단순한 블록 배치 (일부 앱 브라우저에서 글자가 잘리지 않게) */
.bin .body { padding: 14px 16px 16px; display: block; }
.bin .body > * + * { margin-top: 12px; }
.bin ul { list-style: none; margin: 0; padding: 0; }
.bin li { display: block; }
.bin li + li { margin-top: 8px; }
.bin li b { display: block; font-weight: 700; }
.bin li em { display: block; font-style: normal; color: var(--muted); font-size: 14px; }
.rule {
  display: block; height: auto; overflow: visible;
  font-size: 14px; line-height: 1.6; padding: 10px 12px; border-radius: 8px; background: var(--ok-bg);
}
.never {
  display: block; height: auto; overflow: visible;
  font-size: 14px; line-height: 1.6; padding: 10px 12px; border-radius: 8px; background: var(--no-bg); color: var(--no-ink);
}
.rule b, .never b { display: block; margin-bottom: 2px; }

/* Quiz */
.quiz { display: flex; flex-direction: column; gap: 10px; }
details {
  background: var(--surface); border: 1px solid var(--line); border-radius: 10px; padding: 0 16px;
}
summary {
  cursor: pointer; padding: 14px 0; font-weight: 700; list-style: none;
  display: flex; justify-content: space-between; gap: 12px; align-items: center;
}
summary::-webkit-details-marker { display: none; }
summary::after { content: "정답 보기"; font-size: 13px; font-weight: 500; color: var(--accent); white-space: nowrap; }
details[open] summary::after { content: "접기"; }
summary:focus-visible { outline: 2px solid var(--focus); outline-offset: 2px; border-radius: 4px; }
details p { margin: 0 0 14px; }
details .ans { font-family: var(--display); font-size: 18px; }

footer { color: var(--muted); font-size: 13px; border-top: 1px solid var(--line); padding-top: 16px; }
footer p { margin: 0 0 4px; }

@media (prefers-reduced-motion: reduce) { * { transition: none !important; scroll-behavior: auto !important; } }
</style>
</head>
<body>
<main class="wrap">
  <section>
    <p class="eyebrow">신현고 체인지 메이커 - 분리배출 스테이션</p>
    <h1>이거 어디 버려?</h1>
    <p class="lede">손에 든 쓰레기 이름을 검색하면 어느 수거함에 넣을지 바로 알려줘요. 버리기 전에 3초만 확인해 주세요.</p>
  </section>

  <div class="here" id="here" hidden></div>

  <section class="search" aria-label="품목 검색">
    <label for="q">무엇을 버리나요?</label>
    <input id="q" type="search" placeholder="예: 우유팩, 페트병, 컵라면" autocomplete="off">
    <div class="chips" id="chips" aria-label="자주 찾는 품목"></div>
    <div class="results" id="results" aria-live="polite"></div>
    <a class="ai-link" href="ai.html">카메라로 AI에게 물어보기</a>
  </section>

  <section aria-labelledby="bins-title">
    <h2 id="bins-title">수거함별 안내</h2>
    <div class="bins" id="bins"></div>
  </section>

  <section aria-labelledby="quiz-title">
    <h2 id="quiz-title">자주 틀리는 것 6가지</h2>
    <div class="quiz" id="quiz"></div>
  </section>

  <footer>
    <p>체인지메이커 분리배출 스테이션 프로젝트</p>
  </footer>
</main>

<script>
const BINS = {
  plastic: { name: "플라스틱", sub: "페트병 · 플라스틱 용기", color: "var(--plastic)",
    rule: "내용물을 비우고, 헹구고, 라벨을 떼고, 찌그러뜨려서 넣어요",
    never: "빨대 · 플라스틱 숟가락처럼 작은 것, 음식물이 지워지지 않는 용기" },
  can: { name: "캔 · 고철", sub: "음료캔 · 통조림캔", color: "var(--can)",
    rule: "내용물을 비우고, 가볍게 헹군 뒤, 납작하게 찌그러뜨려서 넣어요",
    never: "음료가 남은 캔, 쓰레기를 넣은 캔" },
  paper: { name: "종이류", sub: "종이 · 우유팩 · 종이컵", color: "var(--paper)",
    rule: "테이프 · 스프링 · 비닐 떼기. 우유팩과 종이컵은 헹군 뒤 일반 종이와 따로 모아 주세요",
    never: "영수증, 코팅된 종이, 휴지, 기름이나 음식이 묻은 종이" },
  general: { name: "일반쓰레기", sub: "재활용이 안 되는 것", color: "var(--general)",
    rule: "재활용함에 잘못 들어가면 그 함 전체가 일반쓰레기가 돼요. 애매하면 확인부터!",
    never: "깨끗한 페트병은 플라스틱함, 캔은 캔 · 고철함, 종이는 종이류함에 넣어 주세요" }
};

const ITEMS = [
  { n: "투명 페트병", a: "생수병 음료수병 페트 물병", b: "plastic", t: "비우고 라벨 떼고 찌그러뜨린 뒤 뚜껑 닫기" },
  { n: "플라스틱 음료컵", a: "테이크아웃컵 아이스컵 카페컵", b: "plastic", t: "헹군 뒤 빨대 빼고 넣기" },
  { n: "도시락 · 배달 용기", a: "플라스틱용기 반찬통", b: "plastic", t: "음식물 씻어낸 뒤 넣기" },
  { n: "음료 캔", a: "콜라캔 사이다캔 커피캔 캔음료", b: "can", t: "끝까지 비우고 납작하게" },
  { n: "참치 · 통조림 캔", a: "참치캔 통조림", b: "can", t: "헹구고 뚜껑은 안쪽으로 접어 넣기 (손 조심)" },
  { n: "프린트물 · 시험지", a: "a4 종이 학습지 유인물", b: "paper", t: "스테이플러 심은 떼면 더 좋아요" },
  { n: "공책 · 노트", a: "노트 연습장", b: "paper", t: "스프링과 비닐 표지는 떼기" },
  { n: "택배 상자", a: "박스 골판지 상자", b: "paper", t: "테이프와 송장 떼고 펼쳐서" },
  { n: "우유팩", a: "우유 종이팩 멸균팩 두유", b: "paper", t: "헹궈서 펼친 뒤 일반 종이와 따로" },
  { n: "종이컵", a: "자판기컵 종이 컵", b: "paper", t: "헹군 뒤 우유팩과 같이 모으기" },
  { n: "영수증", a: "영수증 감열지 카드전표", b: "general", t: "특수 코팅 종이라 재활용 안 돼요" },
  { n: "휴지 · 물티슈", a: "티슈 휴지 물티슈 냅킨", b: "general", t: "물티슈는 플라스틱 섬유라 종이가 아니에요" },
  { n: "빨대", a: "빨대 스트로", b: "general", t: "너무 작아서 선별이 안 돼요" },
  { n: "나무젓가락", a: "젓가락 이쑤시개", b: "general", t: "나무는 종이로 재활용되지 않아요" },
  { n: "컵라면 용기", a: "컵라면 라면컵 스티로폼", b: "general", t: "국물이 배어 안 지워지면 일반쓰레기" },
  { n: "과자봉지", a: "과자 봉지 비닐 포장지", b: "general", t: "비닐 수거함이 따로 있으면 그쪽으로" },
  { n: "젤리 봉지", a: "젤리봉지 사탕 봉지", b: "general", t: "비닐 수거함이 따로 있으면 그쪽으로" },
  { n: "아이스크림 봉지", a: "아이스크림봉지 하드 껍질", b: "general", t: "녹은 아이스크림을 털어내고, 막대도 일반쓰레기로" },
  { n: "빵 봉지", a: "빵봉지 빵 포장지 샌드위치", b: "general", t: "부스러기를 털고, 비닐 수거함이 있으면 그쪽으로" },
  { n: "만두 봉지", a: "만두봉지 냉동식품 봉지", b: "general", t: "기름이 묻은 봉지는 비닐로도 재활용이 안 돼요" },
  { n: "볼펜 · 샤프", a: "펜 볼펜 샤프 형광펜", b: "general", t: "여러 재질이 섞여 있어요" },
  { n: "마스크", a: "마스크", b: "general", t: "끈을 잘라서 버려 주세요" },
  { n: "코팅된 종이", a: "코팅지 사진 스티커", b: "general", t: "비닐 코팅은 종이로 재활용 안 돼요" }
];

const QUIZ = [
  { q: "라벨이 붙은 페트병", a: "plastic", w: "라벨을 떼야 플라스틱으로 재활용돼요. 라벨은 일반쓰레기로." },
  { q: "다 마신 우유팩", a: "paper", w: "헹궈서 펼친 뒤 일반 종이와 따로 모아야 해요. 우유팩은 고급 펄프라 따로 재활용돼요." },
  { q: "영수증", a: "general", w: "종이처럼 보이지만 열에 반응하는 코팅 종이라 재활용이 안 돼요." },
  { q: "국물이 밴 컵라면 용기", a: "general", w: "빨간 국물이 안 지워지면 재활용이 안 돼요. 깨끗하면 스티로폼으로." },
  { q: "음료컵에 꽂힌 빨대", a: "general", w: "컵은 플라스틱, 빨대는 일반쓰레기. 빼서 따로 버려요." },
  { q: "과자봉지", a: "general", w: "원래는 비닐류예요. 비닐 수거함이 있으면 거기로, 없으면 일반쓰레기로." }
];

const $ = (s) => document.querySelector(s);
const norm = (s) => s.toLowerCase().replace(/[\s·]/g, "");

function tagHTML(binKey) {
  const b = BINS[binKey];
  return `<div class="tag" style="background:${b.color}">${b.name}</div>`;
}

function renderBins() {
  $("#bins").innerHTML = Object.entries(BINS).map(([key, b]) => {
    const list = ITEMS.filter(i => i.b === key).map(i =>
      `<li><b>${i.n}</b>${i.t ? `<em>${i.t}</em>` : ""}</li>`).join("");
    return `<article class="bin" id="${key}" style="--bin-color:${b.color}">
      <header><h3>${b.name}</h3><span>${b.sub}</span></header>
      <div class="body">
        <div class="rule"><b>이렇게 넣어요</b>${b.rule}</div>
        <ul>${list}</ul>
        <div class="never"><b>${key === "general" ? "여기 말고" : "넣으면 안 돼요"}</b>${b.never}</div>
      </div>
    </article>`;
  }).join("");
}

function renderChips() {
  const picks = ["우유팩", "컵라면", "종이컵", "빨대", "과자봉지", "캔 음료", "아이스크림 봉지", "만두 봉지", "젤리 봉지", "빵 봉지", "페트병", "학습지", "휴지", "나무젓가락"];
  $("#chips").innerHTML = picks.map(p => `<button class="chip" type="button" data-q="${p}">${p}</button>`).join("");
  $("#chips").addEventListener("click", (e) => {
    const btn = e.target.closest("button[data-q]");
    if (!btn) return;
    $("#q").value = btn.dataset.q;
    search();
    $("#q").focus();
  });
}

function search() {
  const q = norm($("#q").value);
  const out = $("#results");
  if (!q) { out.innerHTML = ""; return; }
  const hits = ITEMS.filter(i => norm(i.n + i.a).includes(q));
  if (!hits.length) {
    out.innerHTML = `<p class="empty">아직 목록에 없는 품목이에요. 재질을 확인하고, 애매하면 일반쓰레기 대신 선생님께 물어봐 주세요.</p>`;
    return;
  }
  out.innerHTML = hits.map(i => `<div class="result">${tagHTML(i.b)}<strong>${i.n}</strong><span>${i.t || BINS[i.b].sub}</span></div>`).join("");
}

function renderQuiz() {
  $("#quiz").innerHTML = QUIZ.map(x => `<details>
      <summary>${x.q}</summary>
      <p class="ans" style="color:${BINS[x.a].color}">${BINS[x.a].name}</p>
      <p>${x.w}</p>
    </details>`).join("");
}

function applyHash() {
  const key = (location.hash || "").replace("#", "");
  const here = $("#here");
  document.querySelectorAll(".bin").forEach(el => el.classList.toggle("is-here", el.id === key));
  if (BINS[key]) {
    const b = BINS[key];
    here.style.setProperty("--here-color", b.color);
    here.innerHTML = `<div>지금 「${b.name}」 수거함 앞이에요<small>${b.rule}</small></div>
      <button type="button" class="here-btn" id="here-btn">이 함 안내 보기</button>`;
    here.hidden = false;
    $("#here-btn").addEventListener("click", () => {
      const card = document.getElementById(key);
      if (card) card.scrollIntoView({ block: "start", behavior: "smooth" });
    });
  } else {
    here.hidden = true;
  }
}

renderBins();
renderChips();
renderQuiz();
$("#q").addEventListener("input", search);
window.addEventListener("hashchange", applyHash);
applyHash();
</script>
</body>
</html>
