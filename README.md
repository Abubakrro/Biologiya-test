let testlar = [];

fetch("testlar.json")
  .then(response => response.json())
  .then(data => {
    testlar = data;
    renderTestlar();
  });

function renderTestlar() {
  const form = document.getElementById("testForm");
  testlar.forEach((test, index) => {
    const box = document.createElement("div");
    box.innerHTML = `<p><b>${index + 1}. ${test.savol}</b></p>`;
    test.variantlar.forEach((variant, i) => {
      const id = `q${index}_v${i}`;
      box.innerHTML += `
        <label for="${id}">
          <input type="radio" name="savol${index}" id="${id}" value="${variant}" />
          ${variant}
        </label><br/>
      `;
    });
    form.appendChild(box);
  });
}

document.getElementById("submitBtn").addEventListener("click", () => {
  const resultDiv = document.getElementById("result");
  let togrilar = 0;
  testlar.forEach((test, index) => {
    const tanlangan = document.querySelector(`input[name="savol${index}"]:checked`);
    if (tanlangan && tanlangan.value === test.javob) {
      togrilar++;
    }
  });
  resultDiv.innerHTML = `<h2>Natija: ${togrilar} / ${testlar.length} to‘g‘ri</h2>`;
});biotest/
├── index.html         # Asosiy test sahifasi
├── style.css          # Qorong‘i dizayn uchun CSS
├── script.js          # Testlarni yuklash va natijani hisoblash
└── testlar.json       # Savollar va javoblar kaliti
