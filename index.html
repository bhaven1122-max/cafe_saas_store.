<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Smart Cafe SaaS Platform</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #FBF9F5; color: #1C130E; }
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    @keyframes pulse-border { 0%, 100% { border-color: #ef4444; } 50% { border-color: transparent; } }
    .animate-pulse-red { animation: pulse-border 1.5s infinite; }
  </style>
</head>
<body class="min-h-screen pb-24">

  <div id="app">
    <div class="min-h-screen flex flex-col items-center justify-center font-bold text-amber-800 bg-[#FBF9F5]">
      <div class="w-10 h-10 border-4 border-amber-600 border-t-transparent rounded-full animate-spin mb-3"></div>
      Loading Smart Cafe SaaS... ☕
    </div>
  </div>

  <script>
    const SUPABASE_URL = "https://nkcapgathefgnbnzboiq.supabase.co";
    const SUPABASE_KEY = "Sb_publishable_8Gmh1J9VWeN5SqXPHCqQJA_TvrrMdws";
    const supabaseClient = window.supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

    const SUPER_ADMIN_PIN = "9999";

    const defaultMenuTemplate = [
      { id: 1, name: "Signature Hazelnut Cold Coffee", category: "Coffee", price: 149, is_veg: true, is_bestseller: true, in_stock: true, img: "https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&q=80" },
      { id: 2, name: "Classic Caramel Frappe", category: "Coffee", price: 159, is_veg: true, is_bestseller: false, in_stock: true, img: "https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&q=80" },
      { id: 3, name: "Maharaja Double Cheese Burger", category: "Burgers & Sandwiches", price: 169, is_veg: true, is_bestseller: true, in_stock: true, img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500&q=80" },
      { id: 4, name: "Farmhouse Loaded Cheese Pizza [8 Inch]", category: "Pizza & Pasta", price: 249, is_veg: true, is_bestseller: true, in_stock: true, img: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&q=80" },
      { id: 5, name: "Sizzling Hot Chocolate Brownie", category: "Desserts", price: 179, is_veg: true, is_bestseller: true, in_stock: true, img: "https://images.unsplash.com/photo-1606313564200-e75d5e30476c?w=500&q=80" }
    ];

    const initialSaaSData = {
      cafes: {
        "sukoon": {
          slug: "sukoon",
          cafe_name: "Sukoon The Cafe",
          upi_id: "sukooncafe@upi",
          whatsapp_number: "919876543210",
          chef_pin: "1122",
          owner_pin: "8899",
          total_tables: 10,
          google_review_link: "https://g.page/r/example/review",
          menu: JSON.parse(JSON.stringify(defaultMenuTemplate)),
          orders: [],
          table_status: {}
        }
      }
    };

    let saasDB = null;

    async function loadFromCloud() {
      try {
        const { data } = await supabaseClient.from('cafe_saas_store').select('*').eq('id', 'main_db').single();
        if (data && data.data) saasDB = data.data;
        else { saasDB = initialSaaSData; await saveToCloud(); }
      } catch (err) {
        saasDB = JSON.parse(localStorage.getItem("smart_cafe_db")) || initialSaaSData;
      }
      initApp();
    }

    async function saveToCloud() {
      if (!saasDB) return;
      localStorage.setItem("smart_cafe_db", JSON.stringify(saasDB));
      try {
        await supabaseClient.from('cafe_saas_store').upsert({ id: 'main_db', data: saasDB, updated_at: new Date() });
      } catch (err) {}
    }

    const urlParams = new URLSearchParams(window.location.search);
    let activeCafeSlug = (urlParams.get("cafe") || "sukoon").toLowerCase();
    let currentTable = urlParams.get("table") || "1";

    function currentCafe() {
      if (!saasDB || !saasDB.cafes) return initialSaaSData.cafes["sukoon"];
      if (!saasDB.cafes[activeCafeSlug]) activeCafeSlug = Object.keys(saasDB.cafes)[0] || "sukoon";
      if (!saasDB.cafes[activeCafeSlug].table_status) saasDB.cafes[activeCafeSlug].table_status = {};
      if (!saasDB.cafes[activeCafeSlug].google_review_link) saasDB.cafes[activeCafeSlug].google_review_link = "https://google.com";
      return saasDB.cafes[activeCafeSlug];
    }

    let cart = {};
    let selectedCategory = "All";
    let activeOrderId = null;
    let cartStep = 0;
    let customerName = "";
    let soundEnabled = false;
    let pinUnlocked = false;
    let customerTab = "menu";
    let ownerTab = "sales";

    function setupRealtimeSync() {
      supabaseClient.channel('public:cafe_saas_store')
        .on('postgres_changes', { event: 'UPDATE', schema: 'public', table: 'cafe_saas_store' }, payload => {
          if (payload.new && payload.new.data) {
            saasDB = payload.new.data;
            render();
          }
        }).subscribe();
    }

    function getRoute() {
      const mode = urlParams.get("mode");
      if (mode === "superadmin") return "SUPERADMIN";
      if (mode === "kitchen") return "KDS";
      if (mode === "owner") return "OWNER";
      return "CUSTOMER";
    }

    function renderSuperAdmin() {
      if (!pinUnlocked) {
        return `
          <div class="min-h-screen bg-stone-950 text-white flex items-center justify-center p-4">
            <div class="bg-stone-900 p-8 rounded-3xl max-w-sm w-full text-center border border-amber-500/40 shadow-2xl">
              <h2 class="text-xl font-extrabold text-amber-400 mb-1">🚀 Super Admin Panel</h2>
              <p class="text-xs text-stone-400 mb-6">Enter PIN (9999)</p>
              <input id="superPin" type="password" maxlength="4" placeholder="••••" class="w-full text-center text-3xl tracking-widest bg-stone-800 rounded-2xl py-3 mb-4 text-white border border-stone-700" />
              <button onclick="if(document.getElementById('superPin').value === '9999'){pinUnlocked=true; render();}else{alert('Wrong PIN');}" class="w-full bg-amber-500 text-black font-extrabold py-3.5 rounded-2xl">Unlock</button>
            </div>
          </div>
        `;
      }
      const cafeList = Object.values(saasDB.cafes);
      const baseUrl = window.location.origin + window.location.pathname;

      return `
        <div class="min-h-screen bg-stone-950 text-white p-6">
          <div class="max-w-4xl mx-auto">
            <h1 class="text-2xl font-extrabold text-amber-400 mb-6">🚀 Super Admin Control Center</h1>
            
            <div class="bg-stone-900 p-6 rounded-3xl border border-stone-800 mb-6">
              <h3 class="text-base font-extrabold text-amber-400 mb-3">➕ Create New Cafe</h3>
              <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 mb-3">
                <input id="newSlug" type="text" placeholder="Cafe ID (e.g. taj)" class="bg-stone-800 border border-stone-700 rounded-xl px-3 py-2.5 text-xs text-white" />
                <input id="newName" type="text" placeholder="Cafe Name" class="bg-stone-800 border border-stone-700 rounded-xl px-3 py-2.5 text-xs text-white" />
                <input id="newUpi" type="text" placeholder="UPI ID" class="bg-stone-800 border border-stone-700 rounded-xl px-3 py-2.5 text-xs text-white" />
              </div>
              <button onclick="createNewCafe()" class="bg-amber-500 text-black font-extrabold px-6 py-2.5 rounded-xl text-xs">Create Cafe</button>
            </div>

            <div class="space-y-4">
              ${cafeList.map(c => `
                <div class="bg-stone-900 rounded-3xl p-5 border border-stone-800 flex flex-wrap justify-between items-center gap-4">
                  <div>
                    <h3 class="text-lg font-extrabold text-white">${c.cafe_name} <span class="text-xs text-amber-400 font-mono">(${c.slug})</span></h3>
                    <p class="text-xs text-stone-400">Chef PIN: <b>${c.chef_pin}</b> | Owner PIN: <b>${c.owner_pin}</b></p>
                  </div>
                  <div class="flex gap-2 text-xs">
                    <a href="${baseUrl}?cafe=${c.slug}&table=1" target="_blank" class="bg-amber-600/20 text-amber-300 px-3 py-2 rounded-xl font-bold">Menu ↗</a>
                    <a href="${baseUrl}?cafe=${c.slug}&mode=kitchen" target="_blank" class="bg-green-600/20 text-green-300 px-3 py-2 rounded-xl font-bold">KDS ↗</a>
                    <a href="${baseUrl}?cafe=${c.slug}&mode=owner" target="_blank" class="bg-purple-600/20 text-purple-300 px-3 py-2 rounded-xl font-bold">Owner ↗</a>
                  </div>
                </div>
              `).join('')}
            </div>
          </div>
        </div>
      `;
    }

    function createNewCafe() {
      const slug = (document.getElementById("newSlug").value || "").trim().toLowerCase();
      const name = (document.getElementById("newName").value || "").trim();
      const upi = (document.getElementById("newUpi").value || "").trim() || "cafe@upi";
      if (!slug || !name) return alert("Fill ID & Name!");
      saasDB.cafes[slug] = {
        slug, cafe_name: name, upi_id: upi, whatsapp_number: "919876543210", chef_pin: "1122", owner_pin: "8899", total_tables: 10,
        google_review_link: "https://google.com", menu: JSON.parse(JSON.stringify(defaultMenuTemplate)), orders: [], table_status: {}
      };
      saveToCloud(); render(); alert("Created successfully!");
    }

    function renderCustomer() {
      const cafe = currentCafe();
      const menu = cafe.menu;
      const categories = ["All", ...new Set(menu.map(i => i.category))];
      const filtered = menu.filter(i => selectedCategory === "All" || i.category === selectedCategory);
      const cartItems = Object.values(cart);
      const totalQty = cartItems.reduce((s, i) => s + i.qty, 0);
      const grandTotal = cartItems.reduce((s, i) => s + (i.price * i.qty), 0);
      const activeOrder = cafe.orders.find(o => o.id === activeOrderId);

      return `
        <header class="sticky top-0 z-30 bg-[#1C130E] text-[#FBF9F5] px-4 py-3.5 shadow-xl">
          <div class="max-w-xl mx-auto flex items-center justify-between">
            <h1 class="text-base font-extrabold text-amber-400">${cafe.cafe_name}</h1>
            <div class="bg-stone-800 px-3 py-1.5 rounded-full text-xs font-bold text-amber-300">
              Table #${currentTable}
            </div>
          </div>
        </header>

        <main class="max-w-xl mx-auto px-4 pt-4 pb-28">
          ${customerTab === 'menu' ? `
            ${activeOrder ? `
              <div class="mb-4 bg-white rounded-3xl p-4 shadow border-2 border-amber-500 text-xs">
                <div class="font-extrabold text-amber-900 mb-2">Order #${activeOrder.order_number} Status: <b class="text-green-700">${activeOrder.order_status.toUpperCase()}</b></div>
                <a href="${cafe.google_review_link}" target="_blank" class="block text-center bg-amber-50 text-amber-900 font-bold py-2 rounded-xl mt-2 border border-amber-300">⭐ Rate us on Google!</a>
              </div>
            ` : ''}

            <div class="flex gap-2 overflow-x-auto no-scrollbar pb-3 mb-2">
              ${categories.map(cat => `<button onclick="selectedCategory='${cat}'; render()" class="whitespace-nowrap px-4 py-2 rounded-full text-xs font-bold ${selectedCategory === cat ? 'bg-[#1C130E] text-amber-400' : 'bg-white text-stone-700 border'}">${cat}</button>`).join('')}
            </div>

            <div class="space-y-3">
              ${filtered.map(item => {
                const inCart = cart[item.id]?.qty || 0;
                return `
                  <div class="bg-white rounded-3xl p-3.5 shadow-sm border flex gap-3.5 items-center ${!item.in_stock ? 'opacity-60 bg-stone-100' : ''}">
                    <img src="${item.img}" class="w-20 h-20 rounded-2xl object-cover bg-stone-100 flex-shrink-0" />
                    <div class="flex-1 min-w-0">
                      <h3 class="font-extrabold text-sm text-stone-900 truncate">${item.name}</h3>
                      <p class="font-extrabold text-base text-stone-900 mt-1">₹${item.price}</p>
                      ${!item.in_stock ? '<span class="text-[10px] font-bold text-red-600 bg-red-100 px-2 py-0.5 rounded-full">🔴 Sold Out</span>' : ''}
                    </div>
                    <div>
                      ${item.in_stock ? (inCart === 0 ? `<button onclick="updateCart(${item.id}, 1)" class="bg-amber-50 border border-amber-500 font-extrabold text-xs px-4 py-2.5 rounded-2xl">+ ADD</button>` : `<div class="flex items-center bg-[#1C130E] text-white rounded-2xl overflow-hidden"><button onclick="updateCart(${item.id}, -1)" class="px-3 py-2 text-amber-400 font-bold">-</button><span class="px-2.5 text-xs font-extrabold">${inCart}</span><button onclick="updateCart(${item.id}, 1)" class="px-3 py-2 text-amber-400 font-bold">+</button></div>`) : '<span class="text-xs font-bold text-stone-400">Unavailable</span>'}
                    </div>
                  </div>
                `;
              }).join('')}
            </div>
          ` : customerTab === 'cart' ? `
            <div class="bg-white p-5 rounded-3xl shadow-sm border text-xs">
              <h2 class="font-extrabold text-base text-stone-900 mb-3">🛒 Your Cart (Table #${currentTable})</h2>
              ${cartItems.length === 0 ? '<p class="text-stone-400 py-8 text-center">Your cart is empty.</p>' : `
                <div class="divide-y mb-4">${cartItems.map(i => `<div class="py-2.5 flex justify-between"><span>${i.qty}x ${i.name}</span><b>₹${i.price * i.qty}</b></div>`).join('')}</div>
                <div class="font-extrabold text-sm mb-4">Total: ₹${grandTotal}</div>
                <input type="text" placeholder="Your Name (Optional)" value="${customerName}" oninput="customerName=this.value" class="w-full border rounded-2xl px-4 py-3 mb-4" />
                <button onclick="placeOrder(${grandTotal})" class="w-full bg-[#1C130E] text-amber-400 font-extrabold py-4 rounded-2xl text-sm shadow">🔔 Send to Kitchen & WhatsApp</button>
              `}
            </div>
          ` : customerTab === 'summary' ? `
            <div class="bg-white p-5 rounded-3xl shadow-sm border text-xs">
              <h2 class="font-extrabold text-base text-stone-900 mb-3">📋 Order Summary</h2>
              ${cafe.orders.filter(o => o.table_number === currentTable).length === 0 ? '<p class="text-stone-400 py-8 text-center">No active orders for this table.</p>' : `
                <div class="space-y-3">${cafe.orders.filter(o => o.table_number === currentTable).map(o => `
                  <div class="p-3 bg-stone-50 rounded-2xl border">
                    <div class="font-extrabold text-amber-900">Order #${o.order_number} — Status: <b class="text-green-700">${o.order_status.toUpperCase()}</b></div>
                    <div class="text-stone-600 mt-1">${o.items.map(i => `${i.qty}x ${i.name}`).join(', ')}</div>
                    <div class="font-bold mt-1">Total: ₹${o.total_amount}</div>
                  </div>
                `).join('')}</div>
              `}
            </div>
          ` : `
            <div class="bg-white p-6 rounded-3xl shadow-sm border text-center space-y-4">
              <h2 class="font-extrabold text-base text-stone-900">🔔 Bell to Chef / Call Waiter</h2>
              <p class="text-xs text-stone-500">Need water, extra tissue, or help at Table #${currentTable}? Click below to alert the kitchen instantly!</p>
              <button onclick="alert('🔔 Waiter alerted for Table #${currentTable}! Someone is coming.')" class="w-full bg-amber-600 hover:bg-amber-500 text-white font-extrabold py-4 rounded-2xl text-sm shadow">🔔 Ring Bell for Table #${currentTable}</button>
            </div>
          `}
        </main>

        <!-- Bottom Navigation Bar -->
        <nav class="fixed bottom-0 left-0 right-0 bg-[#1C130E] text-stone-400 flex justify-around py-3 px-2 border-t border-stone-800 z-40 text-xs font-bold">
          <button onclick="customerTab='menu'; render()" class="flex flex-col items-center ${customerTab==='menu'?'text-amber-400':''}"><span>📖</span>Menu</button>
          <button onclick="customerTab='cart'; render()" class="flex flex-col items-center relative ${customerTab==='cart'?'text-amber-400':''}"><span>🛒</span>Cart ${totalQty>0?`(${totalQty})`:''}</button>
          <button onclick="customerTab='summary'; render()" class="flex flex-col items-center ${customerTab==='summary'?'text-amber-400':''}"><span>📋</span>Summary</button>
          <button onclick="customerTab='bell'; render()" class="flex flex-col items-center ${customerTab==='bell'?'text-amber-400':''}"><span>🔔</span>Bell to Chef</button>
        </nav>
      `;
    }

    function updateCart(id, delta) {
      const item = currentCafe().menu.find(x => x.id === id);
      if (!item || !item.in_stock) return;
      if (!cart[id]) cart[id] = { ...item, qty: 0 };
      cart[id].qty += delta;
      if (cart[id].qty <= 0) delete cart[id];
      render();
    }

    function placeOrder(total) {
      const cafe = currentCafe();
      const cartItems = Object.values(cart);
      const newOrder = {
        id: "ord_" + Date.now(), order_number: Math.floor(100 + Math.random() * 900), table_number: currentTable,
        customer_name: customerName || "Guest", items: cartItems.map(i => ({ name: i.name, price: i.price, qty: i.qty })),
        total_amount: total, order_status: "new", created_at: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
      };
      cafe.orders.unshift(newOrder);
      if(!cafe.table_status) cafe.table_status = {};
      cafe.table_status[currentTable] = "Occupied";
      activeOrderId = newOrder.id;

      const waText = encodeURIComponent(`*New Order #${newOrder.order_number}* (Table #${currentTable})\nCustomer: ${newOrder.customer_name}\n\n` + cartItems.map(i => `- ${i.qty}x ${i.name} (₹${i.price * i.qty})`).join('\n') + `\n\n*Total: ₹${total}*`);
      window.open(`https://wa.me/${cafe.whatsapp_number}?text=${waText}`, '_blank');

      cart = {}; customerTab = 'summary'; saveToCloud(); render();
    }

    function renderKDS() {
      const cafe = currentCafe();
      if (!pinUnlocked) {
        return `
          <div class="min-h-screen bg-[#1C130E] text-white flex items-center justify-center p-4">
            <div class="bg-stone-900 p-8 rounded-3xl max-w-sm w-full text-center border">
              <h2 class="text-xl font-extrabold text-amber-400 mb-1">👨‍🍳 Kitchen KDS</h2>
              <p class="text-xs text-stone-400 mb-6">Enter Chef PIN (${cafe.chef_pin})</p>
              <input id="pinInput" type="password" maxlength="4" placeholder="••••" class="w-full text-center text-3xl tracking-widest bg-stone-800 rounded-2xl py-3 mb-4 text-white border" />
              <button onclick="if(document.getElementById('pinInput').value === '${cafe.chef_pin}'){pinUnlocked=true; render(); playKitchenBell();}else{alert('Wrong PIN');}" class="w-full bg-amber-600 py-3.5 rounded-2xl font-extrabold text-black">Unlock</button>
            </div>
          </div>
        `;
      }
      return `
        <div class="min-h-screen bg-stone-950 text-white p-6">
          <div class="max-w-5xl mx-auto flex justify-between items-center pb-4 border-b border-stone-800 mb-6">
            <h1 class="text-xl font-extrabold text-amber-400">👨‍🍳 KDS — ${cafe.cafe_name}</h1>
          </div>
          <div class="max-w-5xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-4">
            ${cafe.orders.length === 0 ? `<p class="text-stone-500 col-span-3 text-center py-12">No orders right now...</p>` : ''}
            ${cafe.orders.map(o => `
              <div class="bg-stone-900 rounded-3xl p-5 border-2 ${o.order_status === 'new' ? 'border-red-500 animate-pulse-red' : 'border-stone-800'} text-xs">
                <div class="flex justify-between font-extrabold text-amber-400 mb-3"><span>Table #${o.table_number}</span><span>#${o.order_number}</span></div>
                <div class="divide-y divide-stone-800 mb-4">${o.items.map(i => `<div class="py-1.5 flex justify-between font-bold text-sm"><span>${i.qty}x ${i.name}</span><span>₹${i.price * i.qty}</span></div>`).join('')}</div>
                ${o.order_status === 'new' ? `<button onclick="updateStatus('${o.id}', 'preparing')" class="w-full bg-amber-600 text-white py-2.5 rounded-xl font-bold mb-2">Start Preparing</button>` : o.order_status === 'preparing' ? `<button onclick="updateStatus('${o.id}', 'ready')" class="w-full bg-green-600 text-white py-2.5 rounded-xl font-bold mb-2">Mark Ready</button>` : `<div class="text-center text-green-400 font-bold py-2 mb-2">✔ Completed</div>`}
                <button onclick="checkoutTable('${o.table_number}')" class="w-full bg-stone-800 hover:bg-stone-700 text-amber-300 py-2 rounded-xl font-bold">🧹 Checkout Table #${o.table_number}</button>
              </div>
            `).join('')}
          </div>
        </div>
      `;
    }

    function playKitchenBell() {
      try {
        const ctx = new (window.AudioContext || window.webkitAudioContext)();
        const osc = ctx.createOscillator(); const gain = ctx.createGain();
        osc.frequency.setValueAtTime(880, ctx.currentTime);
        osc.connect(gain); gain.connect(ctx.destination);
        osc.start(); osc.stop(ctx.currentTime + 0.3);
      } catch(e){}
    }

    function updateStatus(id, st) {
      const o = currentCafe().orders.find(x => x.id === id);
      if (o) { o.order_status = st; saveToCloud(); render(); }
    }

    function checkoutTable(tableNum) {
      const cafe = currentCafe();
      if(!cafe.table_status) cafe.table_status = {};
      cafe.table_status[tableNum] = "Available";
      saveToCloud(); render();
      alert(`Table #${tableNum} checked out successfully!`);
    }

    function renderOwner() {
      const cafe = currentCafe();
      if (!pinUnlocked) {
        return `
          <div class="min-h-screen bg-[#1C130E] text-white flex items-center justify-center p-4">
            <div class="bg-stone-900 p-8 rounded-3xl max-w-sm w-full text-center border">
              <h2 class="text-xl font-extrabold text-amber-400 mb-1">👑 Owner Panel</h2>
              <p class="text-xs text-stone-400 mb-6">Enter Owner PIN (${cafe.owner_pin})</p>
              <input id="ownerPin" type="password" maxlength="4" placeholder="••••" class="w-full text-center text-3xl tracking-widest bg-stone-800 rounded-2xl py-3 mb-4 text-white border" />
              <button onclick="if(document.getElementById('ownerPin').value === '${cafe.owner_pin}'){pinUnlocked=true; render();}else{alert('Wrong PIN');}" class="w-full bg-amber-600 py-3.5 rounded-2xl font-extrabold text-black">Unlock</button>
            </div>
          </div>
        `;
      }
      const totalRev = cafe.orders.reduce((s, o) => s + o.total_amount, 0);
      return `
        <div class="max-w-4xl mx-auto p-6 text-xs">
          <div class="bg-[#1C130E] text-white p-5 rounded-3xl mb-6 flex flex-wrap justify-between items-center gap-4">
            <div>
              <h1 class="text-base font-extrabold text-amber-400">👑 ${cafe.cafe_name} Owner Dashboard</h1>
              <p class="text-stone-300">Total Sales: ₹${totalRev}</p>
            </div>
            <div class="flex gap-2">
              <button onclick="ownerTab='sales'; render()" class="px-3 py-2 rounded-xl font-bold ${ownerTab==='sales'?'bg-amber-500 text-black':'bg-stone-800'}">📊 Sales</button>
              <button onclick="ownerTab='menu'; render()" class="px-3 py-2 rounded-xl font-bold ${ownerTab==='menu'?'bg-amber-500 text-black':'bg-stone-800'}">📖 Menu & Sold Out</button>
            </div>
          </div>

          ${ownerTab === 'sales' ? `
            <div class="bg-white p-5 rounded-3xl border shadow-sm">
              <h3 class="font-extrabold text-sm mb-3">Order History</h3>
              <div class="divide-y">${cafe.orders.length === 0 ? '<p class="py-4 text-stone-400">No orders yet.</p>' : cafe.orders.map(o => `<div class="py-3 flex justify-between"><div><b>Table #${o.table_number}</b> (${o.customer_name})<div class="text-stone-400">${o.created_at}</div></div><b>₹${o.total_amount}</b></div>`).join('')}</div>
            </div>
          ` : `
            <div class="bg-white p-5 rounded-3xl border shadow-sm space-y-4">
              <h3 class="font-extrabold text-sm mb-2">⚙️ Google Review Link & Menu Control (Sold Out / In Stock)</h3>
              <div class="mb-4">
                <label class="font-bold text-stone-700">Google Review URL:</label>
                <input type="text" value="${cafe.google_review_link}" onchange="cafe.google_review_link=this.value; saveToCloud()" class="w-full border rounded-xl p-2.5 mt-1 text-xs" />
              </div>
              <div class="space-y-2">
                ${cafe.menu.map(i => `
                  <div class="flex justify-between items-center p-3 bg-stone-50 rounded-2xl border">
                    <div>
                      <b class="text-stone-900">${i.name}</b>
                      <div class="text-stone-500">₹${i.price} • ${i.category}</div>
                    </div>
                    <button onclick="toggleStock(${i.id})" class="px-3 py-1.5 rounded-xl font-extrabold ${i.in_stock ? 'bg-green-100 text-green-800 border border-green-300' : 'bg-red-100 text-red-800 border border-red-300'}">
                      ${i.in_stock ? '🟢 In Stock' : '🔴 Sold Out'}
                    </button>
                  </div>
                `).join('')}
              </div>
            </div>
          `}
        </div>
      `;
    }

    function toggleStock(id) {
      const cafe = currentCafe();
      const item = cafe.menu.find(x => x.id === id);
      if(item) {
        item.in_stock = !item.in_stock;
        saveToCloud(); render();
      }
    }

    function render() {
      if (!saasDB) return;
      const route = getRoute();
      const root = document.getElementById("app");
      if (route === "SUPERADMIN") root.innerHTML = renderSuperAdmin();
      else if (route === "KDS") root.innerHTML = renderKDS();
      else if (route === "OWNER") root.innerHTML = renderOwner();
      else root.innerHTML = renderCustomer();
    }

    function initApp() {
      render();
      setupRealtimeSync();
    }

    window.addEventListener("hashchange", () => { pinUnlocked = false; render(); });
    loadFromCloud();
  </script>
</body>
</html>
