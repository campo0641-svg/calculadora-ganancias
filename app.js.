(() => {
  const $ = (id) => document.getElementById(id);
  const costo = $('costo'), precio = $('precio');
  const cop = new Intl.NumberFormat('es-CO', { maximumFractionDigits: 0 });
  const pct = new Intl.NumberFormat('es-CO', { maximumFractionDigits: 1 });

  const leer = (el) => Number(el.value.replace(/\D/g, '')) || 0;

  function formatear(el) {
    const n = leer(el);
    el.value = n ? cop.format(n) : '';
  }

  function calcular() {
    const c = leer(costo), p = leer(precio);
    const caja = $('resultado');
    if (!c && !p) return mostrar(caja, 'vacio', 'Ingresa costo y precio para ver tu ganancia', 0, null, null, 0);

    const g = p - c;
    const rent = c > 0 ? (g / c) * 100 : null;
    const marg = p > 0 ? (g / p) * 100 : null;

    let estado, texto;
    if (g < 0) { estado = 'perdida'; texto = 'Estás perdiendo dinero'; }
    else if (g === 0) { estado = 'baja'; texto = 'Sin ganancia: solo recuperas el costo'; }
    else if (marg !== null && marg < 20) { estado = 'baja'; texto = 'Ganancia baja'; }
    else { estado = 'ganancia'; texto = 'Buena ganancia'; }

    mostrar(caja, estado, texto, g, rent, marg, Math.max(0, Math.min(100, marg ?? 0)));
  }

  function mostrar(caja, estado, texto, g, rent, marg, barra) {
    caja.dataset.estado = estado;
    $('estado').textContent = texto;
    $('ganancia').textContent = (g < 0 ? '-$ ' : '$ ') + cop.format(Math.abs(g));
    $('rentabilidad').textContent = rent === null ? '—' : pct.format(rent) + ' %';
    $('margen').textContent = marg === null ? '—' : pct.format(marg) + ' %';
    $('barra').style.width = barra + '%';
  }

  [costo, precio].forEach((el) => el.addEventListener('input', () => { formatear(el); calcular(); }));
  $('limpiar').addEventListener('click', () => { costo.value = ''; precio.value = ''; calcular(); costo.focus(); });
  calcular();
})();
