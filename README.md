<script>
  const input = document.getElementById('input');
  const f1 = document.getElementById('fancy1');
  const f2 = document.getElementById('fancy2');

  // Additional fancy outputs
  const f3 = document.createElement('div');
  f3.className = 'fancy';
  f3.id = 'fancy3';
  document.body.appendChild(f3);

  const f4 = document.createElement('div');
  f4.className = 'fancy';
  f4.id = 'fancy4';
  document.body.appendChild(f4);

  const f5 = document.createElement('div');
  f5.className = 'fancy';
  f5.id = 'fancy5';
  document.body.appendChild(f5);

  document.body.innerHTML += `
    <button onclick="copyText('fancy3')">Copy Fancy 3</button>
    <button onclick="copyText('fancy4')">Copy Fancy 4</button>
    <button onclick="copyText('fancy5')">Copy Fancy 5</button>
  `;

  input.addEventListener('input', () => {
    const val = input.value;

    // Fancy 1 - Math Sans Serif
    f1.textContent = transform(val, '𝐀');

    // Fancy 2 - Emoji sparkle
    f2.textContent = val.split('').map(c => c + '✨').join('');

    // Fancy 3 - Bold Script
    f3.textContent = transform(val, '𝓐');

    // Fancy 4 - Fraktur
    f4.textContent = transform(val, '𝔄');

    // Fancy 5 - Bubble text
    f5.textContent = val.split('').map(bubbleChar).join('');
  });

  function copyText(id) {
    const text = document.getElementById(id).textContent;
    navigator.clipboard.writeText(text);
    alert('Copied: ' + text);
  }

  function transform(text, baseChar) {
    const base = baseChar.codePointAt(0);
    return text.split('').map(c => {
      const code = c.toUpperCase().charCodeAt(0);
      if (code >= 65 && code <= 90) {
        return String.fromCodePoint(base + (code - 65));
      }
      return c;
    }).join('');
  }

  function bubbleChar(c) {
    const base = 'ⓐ'.codePointAt(0);
    const offset = c.toLowerCase().charCodeAt(0) - 97;
    if (offset >= 0 && offset < 26) return String.fromCodePoint(0x24D0 + offset);
    return c;
  }
</script>