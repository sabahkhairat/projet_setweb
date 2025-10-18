<!doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>متجر إلكتروني - Template</title>
  <style>
    /* ====== Reset & base ====== */
    :root{--accent:#0ea5a4;--dark:#0f172a;--muted:#6b7280}
    *{box-sizing:border-box;margin:0;padding:0}
    body{font-family:Inter, system-ui, Arial;line-height:1.4;background:#f7fafc;color:#111}
    a{color:inherit;text-decoration:none}

    /* ====== Header ====== */
    header{background:#fff;padding:18px 20px;display:flex;align-items:center;justify-content:space-between;gap:12px;border-bottom:1px solid #e6eef2}
    .brand{display:flex;align-items:center;gap:12px}
    .logo{width:48px;height:48px;border-radius:8px;background:linear-gradient(135deg,var(--accent),#7dd3fc);display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700}
    .search{flex:1;max-width:560px}
    .search input{width:100%;padding:10px 12px;border:1px solid #e2e8f0;border-radius:10px}
    .icons{display:flex;gap:12px;align-items:center}
    .cart-btn{position:relative;padding:8px 12px;border-radius:8px;background:#0ea5a4;color:#fff;border:none;cursor:pointer}
    .cart-count{position:absolute;top:-6px;left:-6px;background:#ef4444;color:#fff;border-radius:50%;width:20px;height:20px;display:flex;align-items:center;justify-content:center;font-size:12px}

    /* ====== Layout ====== */
    .container{max-width:1100px;margin:22px auto;padding:0 18px}
    .filters{display:flex;gap:12px;flex-wrap:wrap;margin-bottom:18px}
    .filter-btn{padding:8px 12px;border-radius:999px;border:1px solid #e2e8f0;background:#fff;cursor:pointer}

    /* ====== Products grid ====== */
    .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:16px}
    .card{background:#fff;border-radius:12px;padding:12px;border:1px solid #eef2f6;display:flex;flex-direction:column;gap:8px}
    .card img{width:100%;height:160px;object-fit:cover;border-radius:8px}
    .card h3{font-size:16px}
    .price{font-weight:700;color:var(--dark)}
    .card .actions{margin-top:auto;display:flex;gap:8px}
    .btn{padding:8px 10px;border-radius:8px;border:none;cursor:pointer}
    .btn-outline{background:#fff;border:1px solid #cbd5e1}
    .btn-primary{background:var(--accent);color:#fff}

    /* ====== Cart sidebar ====== */
    .cart-side{position:fixed;top:0;right:0;height:100vh;width:360px;max-width:95%;background:#fff;box-shadow:-8px 0 24px rgba(15,23,42,0.06);transform:translateX(110%);transition:transform .28s ease;padding:18px;z-index:60}
    .cart-side.open{transform:translateX(0)}
    .cart-item{display:flex;gap:10px;align-items:center;padding:8px 0;border-bottom:1px solid #f1f5f9}
    .cart-item img{width:64px;height:64px;object-fit:cover;border-radius:8px}
    .qty-control{display:flex;gap:6px;align-items:center}

    /* ====== Modal ====== */
    .modal{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(2,6,23,0.5);z-index:70}
    .modal.open{display:flex}
    .modal-card{width:100%;max-width:760px;background:#fff;padding:18px;border-radius:12px}
    .modal-content{display:flex;gap:18px;align-items:flex-start}
    .modal-content img{width:320px;height:240px;object-fit:cover;border-radius:8px}

    /* ====== Footer ====== */
    footer{margin-top:26px;padding:18px;text-align:center;color:var(--muted)}

    /* ====== Responsive ====== */
    @media (max-width:720px){
      .modal-content{flex-direction:column}
      .card img{height:140px}
      header{flex-wrap:wrap}
      .search{order:3;width:100%}
    }
    .card .desc {
  color: #6b7280;
  font-size: 14px;
  margin-bottom: 6px;
}

  </style>
</head>
<body>
  <header>
    <div class="brand">
      <div class="logo">E</div>
      <div>
        <div style="font-weight:700">متجر الكتروني</div>
        <div style="font-size:12px;color:#6b7280"> تجارة إلكترونية </div>
      </div>
    </div>

    <div class="search">
      <input id="searchInput" placeholder="قلب هنا على المنتج..." />
    </div>

    <div class="icons">
      <button class="cart-btn" id="openCart">عربة التسوق <span class="cart-count" id="cartCount">0</span></button>
    </div>
  </header>

  <main class="container">
    <div class="filters">
      <button class="filter-btn" data-cat="all">الكل</button>
      <button class="filter-btn" data-cat="home">المنزل</button>
      <button class="filter-btn" data-cat="electronics">الإلكترونيات</button>
      <button class="filter-btn" data-cat="fashion">الأزياء</button>
      <button class="filter-btn" data-cat="beauty">الجمال</button>
    </div>

    <section id="products" class="grid"></section>

    <footer>حقوق الطبع © 2025 - قالب متجر بسيط جاهز للعرض على خمسات</footer>
  </main>

  <!-- Cart sidebar -->
  <aside class="cart-side" id="cartSide">
    <h3>عربة التسوق</h3>
    <div id="cartItems"></div>
    <div style="margin-top:12px;display:flex;justify-content:space-between;align-items:center">
      <strong>المجموع:</strong>
      <strong id="cartTotal">0 د.م</strong>
    </div>
    <div style="margin-top:12px;display:flex;gap:8px">
      <button id="checkoutBtn" class="btn btn-primary">إتمام الطلب (نموزجي)</button>
      <button id="clearCart" class="btn btn-outline">تفريغ العربة</button>
    </div>
  </aside>

  <!-- Modal product -->
  <div class="modal" id="productModal">
    <div class="modal-card">
      <button id="closeModal" style="float:left" class="btn btn-outline">إغلاق</button>
      <div class="modal-content" id="modalContent"></div>
    </div>
  </div>

  <script>
    // ====== بيانات منتجات نموذجية ======
    const products = [
      {id:1,name:'مقلمة ',price:89,cat:'home',img:'image/mialma.jpg', desc :"أضف لمسة من الأناقة والتنظيم إلى مكتبك مع هذه المقلمة العصرية"},
      {id:2,name:'سماعات لاسلكية',price:399,cat:'electronics',img:'image/cite.jpg', desc :"سماعات لاسلكية بصوت نقي واتصال سريع، مثالية للموسيقى والمكالمات"},
      {id:3,name:'تيشيرت 100% قطن',price:149,cat:'fashion',img:'image/tichort.jpg', desc :"تيشيرت قطن مريح بخامة ناعمة وتصميم عصري يناسب جميع الإطلالات"},
      {id:4,name:'عطر أنيق',price:259,cat:'beauty',img:'image/perfun.jpg', desc :"استمتع برائحة فاخرة تدوم طويلاً مع هذا العطر الأنيق."},
      {id:5,name:'مصباح مكتب',price:179,cat:'home',img:'image/lamba.jpg', desc :"مصباح مكتب عصري بتصميم بسيط وإضاءة مريحة للعين"},
      {id:6,name:'شاحن سريع',price:129,cat:'electronics',img:'image/charg.jpg', desc :"اشحن أجهزتك في وقت قياسي مع هذا الشاحن السريع والآمن."}
    ];

    // ====== State ======
    let cart = JSON.parse(localStorage.getItem('cart_v1')) || [];

    // ====== Helpers ======
    const q = s => document.querySelector(s);
    const qA = s => document.querySelectorAll(s);

    function renderProducts(list){
  const el = q('#products');
  el.innerHTML = '';
  list.forEach(p=>{
    const card = document.createElement('article');
    card.className='card';
    card.innerHTML = `
      <img src="${p.img}" alt="${p.name}" />
      <h3>${p.name}</h3>
      <p class="desc">${p.desc}</p>   <!-- هاد السطر زيدي باش يبان الوصف -->
      <div class="price">${p.price} د.م</div>
      <div class="actions">
        <button class="btn btn-outline" data-id="${p.id}" data-action="view">عرض</button>
        <button class="btn btn-primary" data-id="${p.id}" data-action="add">أضف للعربة</button>
      </div>
    `;
    el.appendChild(card);
  });
}


    function openCart(){q('#cartSide').classList.add('open');}
    function closeCart(){q('#cartSide').classList.remove('open');}

    function saveCart(){localStorage.setItem('cart_v1',JSON.stringify(cart));}

    function renderCart(){
      const el = q('#cartItems'); el.innerHTML='';
      let total=0;
      cart.forEach(item=>{
        const product = products.find(p=>p.id===item.id);
        total += product.price * item.qty;
        const div = document.createElement('div');
        div.className='cart-item';
        div.innerHTML = `
          <img src="${product.img}" />
          <div style="flex:1">
            <div style="font-weight:700">${product.name}</div>
            <div style="color:#6b7280">${product.price} د.م</div>
            <div class="qty-control">
              <button class="btn btn-outline" data-id="${item.id}" data-action="dec">-</button>
              <span style="padding:0 8px">${item.qty}</span>
              <button class="btn btn-outline" data-id="${item.id}" data-action="inc">+</button>
            </div>
          </div>
          <div style="text-align:left;font-weight:700">${product.price * item.qty} د.م</div>
        `;
        el.appendChild(div);
      });
      q('#cartTotal').textContent = total + ' د.م';
      q('#cartCount').textContent = cart.reduce((s,i)=>s+i.qty,0);
      saveCart();
    }

    function addToCart(id){
      const found = cart.find(i=>i.id===id);
      if(found) found.qty++;
      else cart.push({id,qty:1});
      renderCart();
      openCart();
    }

    function changeQty(id,delta){
      const it = cart.find(i=>i.id===id); if(!it) return;
      it.qty += delta; if(it.qty<=0) cart = cart.filter(x=>x.id!==id);
      renderCart();
    }

    function clearCart(){cart=[];renderCart();}

    function showProduct(id){
const p = products.find(x=>x.id===id);
q('#modalContent').innerHTML = `
<img src="${p.img}" />
<div>
<h2>${p.name}</h2>
<p style="color:#6b7280">فئة: ${p.cat}</p>
<p style="font-weight:700;margin-top:8px">${p.price} د.م</p>
<p style="margin-top:12px">وصف نموذجي للمنتج. يمكن تغييره بسهولة من ملف HTML (مصفوفة products).</p>
<div style="margin-top:12px;display:flex;gap:8px">
<button class="btn btn-primary" id="modalAdd">أضف للعربة</button>
<button class="btn btn-outline" id="modalClose">إغلاق</button>
</div>
</div>
`;
q('#productModal').classList.add('open');
q('#modalAdd').onclick = ()=>{ addToCart(id); q('#productModal').classList.remove('open'); };
q('#modalClose').onclick = ()=> q('#productModal').classList.remove('open');
}


// ====== Event delegation for products ======
q('#products').addEventListener('click', e=>{
const btn = e.target.closest('button'); if(!btn) return;
const id = Number(btn.dataset.id); const action = btn.dataset.action;
if(action==='add') addToCart(id);
if(action==='view') showProduct(id);
});


// ====== Filters & search ======
qA('.filter-btn').forEach(b=>b.addEventListener('click', ()=>{
const cat = b.dataset.cat;
if(cat==='all') renderProducts(products);
else renderProducts(products.filter(p=>p.cat===cat));
}));


q('#searchInput').addEventListener('input', e=>{
const qv = e.target.value.trim().toLowerCase();
renderProducts(products.filter(p=>p.name.toLowerCase().includes(qv)));
});


// ====== Cart interactions ======
q('#openCart').addEventListener('click', openCart);
q('#cartSide').addEventListener('click', e=>{ if(e.target===q('#cartSide')) closeCart(); });
q('#cartItems').addEventListener('click', e=>{
const btn = e.target.closest('button'); if(!btn) return;
const id = Number(btn.dataset.id); const action = btn.dataset.action;
if(action==='inc') changeQty(id,1);
if(action==='dec') changeQty(id,-1);
});


q('#clearCart').addEventListener('click', clearCart);
q('#checkoutBtn').addEventListener('click', ()=>{
alert('هذا فقط نموذج للواجهة. ربط الدفع يحتاج باكِند.');
});


// ====== Modal close ======
q('#closeModal').addEventListener('click', ()=> q('#productModal').classList.remove('open'));


// ====== Initialize ======
renderProducts(products);
renderCart();


  </script>
</body>
</html>
