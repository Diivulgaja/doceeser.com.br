<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Cardápio - [NOME DA LOJA]</title>
  <!-- Tailwind CDN for quick styling (editable) -->
  <script src="https://cdn.tailwindcss.com"></script>
  <meta name="description" content="Cardápio digital de doces - editável" />
  <style>
    /* Small custom overrides */
    :root{
      --accent-pink:#F7C6D2;
      --accent-cream:#FFF6E6;
      --accent-brown:#8B5E3C;
    }
    .brand-color{background:linear-gradient(90deg,var(--accent-pink),var(--accent-cream));}
  </style>
</head>
<body class="min-h-screen bg-gradient-to-b from-white to-[#FFF8F6] text-[#3b2f2a]">
  <!-- ========== CONFIG (edite aqui) ========== -->
  <script>
    /**
     * CONFIGURAR INFORMAÇÕES DA LOJA AQUI
     */
    const STORE = {
      name: "Doces da Maria",
      description: "Doces artesanais feitos com carinho. Encomendas e entregas.",
      address: "Rua das Flores, 123 - Centro, Sua Cidade - SP",
      hours: "Ter-Sex 9:00–18:00 • Sáb 9:00–14:00",
      whatsapp: "+5511999999999", // sem espaços
      instagram: "docesdamaria",
      pixKey: "000.000.000-00", // chave PIX (CPNJ/telefone/email)
      pixQrPlaceholder: "https://via.placeholder.com/300x300.png?text=QR+PIX"
    };

    /**
     * PRODUTOS - edite ou substitua por chamada API
     * category: 'bolos' | 'brigadeiros' | 'tortas' | 'kits'
     */
    const PRODUCTS = [
      {id:1,category:'bolos',name:'Bolo Red Velvet - Fatia',price:14.50,desc:'Fatia de red velvet com cream cheese',img:'https://images.unsplash.com/photo-1600891964599-f61ba0e24092?auto=format&fit=crop&w=800&q=60'},
      {id:2,category:'brigadeiros',name:'Brigadeiro Gourmet (un)',price:3.50,desc:'Tradicional, cremoso e finalizado com granulado',img:'https://images.unsplash.com/photo-1604908177053-3e2038c3cf0c?auto=format&fit=crop&w=800&q=60'},
      {id:3,category:'tortas',name:'Torta de Limão (fatia)',price:12.00,desc:'Massa crocante e recheio ácido doce',img:'https://images.unsplash.com/photo-1549719389-7a8f0b3f2b6e?auto=format&fit=crop&w=800&q=60'},
      {id:4,category:'kits',name:'Kit Festa - 20 docinhos',price:60.00,desc:'Mix de brigadeiros, beijinhos e cajuzinhos',img:'https://images.unsplash.com/photo-1613187863525-3b63c8c9e0b9?auto=format&fit=crop&w=800&q=60'}
    ];
  </script>

  <!-- ========== HEADER ========== -->
  <header class="py-6 px-6 sm:px-12 flex items-center justify-between">
    <div class="flex items-center gap-4">
      <div class="w-14 h-14 rounded-full brand-color flex items-center justify-center shadow-lg">
        <span class="font-bold text-lg text-[#6b2f2f]">🍰</span>
      </div>
      <div>
        <h1 id="storeName" class="text-2xl font-semibold">Doces da Maria</h1>
        <p id="storeDesc" class="text-sm text-[#5a4a42]">Doces artesanais feitos com carinho.</p>
      </div>
    </div>
    <nav class="hidden md:flex items-center gap-4 text-sm">
      <a href="#menu" class="hover:underline">Cardápio</a>
      <a href="#about" class="hover:underline">Sobre</a>
      <a href="#contact" class="hover:underline">Contato</a>
      <button id="openCartBtn" class="ml-4 bg-[#8B5E3C] text-white px-4 py-2 rounded-lg shadow">Carrinho (<span id="cartCount">0</span>)</button>
    </nav>
  </header>

  <!-- ========== HERO ========== -->
  <section class="px-6 sm:px-12 grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
    <div>
      <h2 class="text-4xl font-extrabold mb-4">Doces artesanais feitos com carinho</h2>
      <p class="mb-6 text-[#5a4a42]">Encomende online para retirada ou delivery. Pagamentos por Pix, cartão ou dinheiro.</p>
      <div class="flex gap-3">
        <a href="#menu" class="px-5 py-3 bg-[#F7C6D2] rounded-lg font-semibold shadow hover:opacity-95">Ver Cardápio</a>
        <a href="#contact" class="px-5 py-3 border rounded-lg">Fazer Encomenda</a>
      </div>
    </div>
    <div class="w-full">
      <img src="https://images.unsplash.com/photo-1548365328-6fd6f3a5b5f8?auto=format&fit=crop&w=900&q=60" alt="doces" class="w-full rounded-2xl shadow-lg" />
    </div>
  </section>

  <!-- ========== MENU / CARDÁPIO ========== -->
  <main id="menu" class="px-6 sm:px-12 py-10">
    <h3 class="text-2xl font-bold mb-4">Cardápio</h3>
    <div class="flex gap-3 mb-6">
      <button data-cat="all" class="category-btn px-3 py-2 rounded-md bg-[#FFF6E6]">Todos</button>
      <button data-cat="bolos" class="category-btn px-3 py-2 rounded-md">Bolos</button>
      <button data-cat="brigadeiros" class="category-btn px-3 py-2 rounded-md">Brigadeiros</button>
      <button data-cat="tortas" class="category-btn px-3 py-2 rounded-md">Tortas</button>
      <button data-cat="kits" class="category-btn px-3 py-2 rounded-md">Kits</button>
    </div>

    <section id="productsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <!-- Produtos renderizados pelo JS -->
    </section>
  </main>

  <!-- ========== ABOUT ========== -->
  <section id="about" class="px-6 sm:px-12 py-8 bg-[#FFF6E6] rounded-lg mx-6 sm:mx-12 mb-8">
    <h4 class="text-xl font-semibold">Sobre a Loja</h4>
    <p id="storeAbout" class="mt-2 text-sm text-[#5a4a42]">Somos uma doceria familiar...</p>
    <div class="mt-4 grid grid-cols-1 md:grid-cols-2 gap-4">
      <div>
        <p><strong>Endereço:</strong> <span id="storeAddress">Rua das Flores, 123</span></p>
        <p><strong>Horário:</strong> <span id="storeHours">Ter-Sex 9-18</span></p>
      </div>
      <div class="flex flex-col gap-2">
        <p><strong>Diferenciais:</strong></p>
        <ul class="list-disc list-inside text-sm">
          <li>Receitas artesanais</li>
          <li>Ingredientes frescos</li>
          <li>Opções personalizadas para festas</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- ========== CONTACT & PAGAMENTOS ========== -->
  <section id="contact" class="px-6 sm:px-12 py-8">
    <h4 class="text-xl font-semibold">Contato e Pagamentos</h4>
    <div class="mt-4 grid grid-cols-1 md:grid-cols-2 gap-6">
      <div>
        <p><strong>WhatsApp:</strong> <a id="whatsappLink" href="#" class="text-[#2a7f5b] underline">Enviar mensagem</a></p>
        <p><strong>Instagram:</strong> <a id="instagramLink" href="#" class="text-[#2a7f5b] underline">@docesdamaria</a></p>
        <p class="mt-4"><strong>PIX</strong></p>
        <div class="mt-2 flex gap-4 items-center">
          <div class="w-36 h-36 border rounded-lg overflow-hidden shadow-sm">
            <img id="pixQr" src="" alt="QR PIX" class="w-full h-full object-cover"/>
          </div>
          <div>
            <p class="text-sm">Chave PIX: <span id="pixKey"></span></p>
            <button id="copyPixBtn" class="mt-2 px-3 py-2 border rounded">Copiar chave PIX</button>
          </div>
        </div>
      </div>

      <div>
        <p><strong>Métodos aceitos</strong></p>
        <ul class="mt-2 list-disc list-inside text-sm">
          <li>Pix (QR e chave)</li>
          <li>Cartão de Crédito / Débito (via link de pagamento)</li>
          <li>Dinheiro (na retirada/entrega)</li>
        </ul>
        <div class="mt-4">
          <p class="text-sm">Ao finalizar, você poderá escolher o método de pagamento. O sistema de cartão aqui é simulado — substitua pelo gateway que preferir (Stripe, Mercado Pago, Pagar.me, Gerencianet, etc.).</p>
        </div>
      </div>
    </div>
  </section>

  <!-- ========== FOOTER ========== -->
  <footer class="px-6 sm:px-12 py-8 border-t mt-8">
    <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
      <div>
        <strong id="footerName">Doces da Maria</strong>
        <p class="text-sm text-[#5a4a42]">© <span id="year"></span> - Todos os direitos</p>
      </div>
      <div class="text-sm">Feito com ❤ · <a href="#contact" class="underline">Fale conosco</a></div>
    </div>
  </footer>

  <!-- ========== CART & CHECKOUT MODAL ========== -->
  <div id="cartModal" class="fixed inset-0 bg-black/40 hidden items-end sm:items-center justify-center z-50">
    <div class="bg-white w-full sm:w-3/4 md:w-1/2 rounded-t-lg sm:rounded-lg p-6 shadow-lg">
      <div class="flex justify-between items-center mb-4">
        <h5 class="text-lg font-bold">Seu Pedido</h5>
        <button id="closeCart" class="text-sm">Fechar ✕</button>
      </div>
      <div id="cartItems" class="space-y-3 max-h-64 overflow-auto mb-4">
        <!-- itens -->
      </div>
      <div class="flex justify-between items-center">
        <strong>Total: R$ <span id="cartTotal">0.00</span></strong>
        <div class="flex gap-3">
          <button id="checkoutBtn" class="px-4 py-2 bg-[#8B5E3C] text-white rounded">Finalizar</button>
        </div>
      </div>
    </div>
  </div>

  <div id="checkoutModal" class="fixed inset-0 bg-black/40 hidden items-end sm:items-center justify-center z-50">
    <div class="bg-white w-full sm:w-3/4 md:w-1/2 rounded-t-lg sm:rounded-lg p-6 shadow-lg">
      <div class="flex justify-between items-center mb-4">
        <h5 class="text-lg font-bold">Finalizar Pedido</h5>
        <button id="closeCheckout" class="text-sm">Fechar ✕</button>
      </div>
      <div class="space-y-4">
        <div>
          <label class="text-sm">Nome</label>
          <input id="buyerName" class="w-full border rounded px-3 py-2 mt-1" placeholder="Seu nome" />
        </div>
        <div>
          <label class="text-sm">Endereço / Retirada</label>
          <input id="buyerAddr" class="w-full border rounded px-3 py-2 mt-1" placeholder="Endereço para entrega ou 'Retirada'" />
        </div>
        <div>
          <label class="text-sm">Método de pagamento</label>
          <select id="payMethod" class="w-full border rounded px-3 py-2 mt-1">
            <option value="pix">Pix (QR / Chave)</option>
            <option value="card">Cartão (link de pagamento)</option>
            <option value="cash">Dinheiro</option>
          </select>
        </div>
        <div id="pixBox" class="border rounded p-3">
          <p class="text-sm">Para pagar com PIX, copie a chave ou escaneie o QR.</p>
          <div class="mt-2 flex gap-4 items-center">
            <div class="w-28 h-28 border rounded overflow-hidden"><img id="pixQr2" src="" alt="PIX QR" class="w-full h-full object-cover"/></div>
            <div>
              <p class="text-sm">Chave: <strong id="pixKey2"></strong></p>
              <button id="copyPixBtn2" class="mt-2 px-3 py-1 border rounded">Copiar chave</button>
            </div>
          </div>
        </div>
        <div id="cardBox" class="hidden border rounded p-3">
          <p class="text-sm">Este é um simulador. Integre um gateway para pagamentos com cartão.</p>
          <input placeholder="Número do cartão" class="w-full border rounded px-3 py-2 mt-2" />
          <div class="flex gap-2 mt-2">
            <input placeholder="MM/AA" class="w-1/3 border rounded px-3 py-2" />
            <input placeholder="CVV" class="w-1/3 border rounded px-3 py-2" />
            <input placeholder="Nome no cartão" class="flex-1 border rounded px-3 py-2" />
          </div>
        </div>
        <div class="flex justify-between items-center">
          <button id="confirmPayment" class="px-4 py-2 bg-[#8B5E3C] text-white rounded">Confirmar Pedido</button>
          <button id="sendWhats" class="px-4 py-2 border rounded">Enviar por WhatsApp</button>
        </div>
      </div>
    </div>
  </div>

  <!-- ========== SCRIPTS ========== -->
  <script>
    // --- Inicialização ---
    document.getElementById('year').textContent = new Date().getFullYear();
    // Preencher dados da loja
    document.getElementById('storeName').textContent = STORE.name;
    document.getElementById('storeDesc').textContent = STORE.description;
    document.getElementById('storeAddress').textContent = STORE.address;
    document.getElementById('storeHours').textContent = STORE.hours;
    document.getElementById('storeAbout').textContent = STORE.description;
    document.getElementById('footerName').textContent = STORE.name;
    document.getElementById('pixKey').textContent = STORE.pixKey;
    document.getElementById('pixKey2').textContent = STORE.pixKey;
    document.getElementById('pixQr').src = STORE.pixQrPlaceholder;
    document.getElementById('pixQr2').src = STORE.pixQrPlaceholder;
    document.getElementById('whatsappLink').href = https://wa.me/${STORE.whatsapp.replace(/[+\s]/g,'')};
    document.getElementById('instagramLink').href = https://instagram.com/${STORE.instagram};

    // --- Render produtos ---
    const grid = document.getElementById('productsGrid');
    function formatPrice(v){ return v.toFixed(2).replace('.',','); }
    function renderProducts(filter='all'){
      grid.innerHTML = '';
      const items = PRODUCTS.filter(p=>filter==='all' ? true : p.category===filter);
      if(items.length===0) grid.innerHTML = '<p class="text-sm text-[#5a4a42]">Nenhum item nesta categoria.</p>';
      items.forEach(p=>{
        const card = document.createElement('article');
        card.className = 'bg-white rounded-lg shadow p-4 flex flex-col';
        card.innerHTML = `
          <img src="${p.img}" alt="${p.name}" class="w-full h-40 object-cover rounded-md mb-3">
          <h5 class="font-semibold">${p.name}</h5>
          <p class="text-sm text-[#5a4a42] mb-2">${p.desc}</p>
          <div class="mt-auto flex items-center justify-between">
            <strong>R$ ${formatPrice(p.price)}</strong>
            <div class="flex gap-2">
              <button class="addBtn px-3 py-1 rounded border" data-id="${p.id}">Adicionar</button>
              <button class="buyNowBtn px-3 py-1 rounded bg-[#F7C6D2]" data-id="${p.id}">Pedir</button>
            </div>
          </div>
        `;
        grid.appendChild(card);
      });

      // ligar eventos
      document.querySelectorAll('.addBtn').forEach(b=>b.addEventListener('click',()=>addToCart(parseInt(b.dataset.id))));
      document.querySelectorAll('.buyNowBtn').forEach(b=>b.addEventListener('click',()=>{ addToCart(parseInt(b.dataset.id)); openCart(); }));
    }
    renderProducts();

    // categorias
    document.querySelectorAll('.category-btn').forEach(btn=>btn.addEventListener('click',()=>{
      document.querySelectorAll('.category-btn').forEach(x=>x.classList.remove('bg-[#FFF6E6]'));
      btn.classList.add('bg-[#FFF6E6]');
      renderProducts(btn.dataset.cat);
    }));

    // --- Carrinho ---
    let CART = [];
    function addToCart(id){
      const prod = PRODUCTS.find(p=>p.id===id);
      const found = CART.find(c=>c.id===id);
      if(found) found.qty += 1; else CART.push({id:prod.id,name:prod.name,price:prod.price,qty:1});
      updateCartUI();
    }
    function updateCartUI(){
      document.getElementById('cartCount').textContent = CART.reduce((s,i)=>s+i.qty,0);
      document.getElementById('cartTotal').textContent = formatPrice(CART.reduce((s,i)=>s+i.price*i.qty,0));
      const container = document.getElementById('cartItems');
      container.innerHTML = '';
      CART.forEach(item=>{
        const el = document.createElement('div');
        el.className = 'flex justify-between items-center border-b pb-2';
        el.innerHTML = `
          <div>
            <div class="font-medium">${item.name}</div>
            <div class="text-sm text-[#5a4a42]">R$ ${formatPrice(item.price)} x ${item.qty}</div>
          </div>
          <div class="flex gap-2">
            <button class="px-2 py-1 border" data-id="${item.id}" data-action="minus">-</button>
            <button class="px-2 py-1 border" data-id="${item.id}" data-action="plus">+</button>
          </div>
        `;
        container.appendChild(el);
      });
      // ligar +/-
      document.querySelectorAll('#cartItems button').forEach(b=>b.addEventListener('click',e=>{
        const id = parseInt(b.dataset.id); const action = b.dataset.action;
        const it = CART.find(c=>c.id===id);
        if(!it) return;
        if(action==='minus'){ it.qty -=1; if(it.qty<=0) CART = CART.filter(x=>x.id!==id);} else it.qty+=1;
        updateCartUI();
      }));
    }

    // abrir/fechar carrinho
    const cartModal = document.getElementById('cartModal');
    function openCart(){ cartModal.classList.remove('hidden'); cartModal.classList.add('flex'); updateCartUI(); }
    function closeCart(){ cartModal.classList.add('hidden'); cartModal.classList.remove('flex'); }
    document.getElementById('openCartBtn').addEventListener('click',openCart);
    document.getElementById('closeCart').addEventListener('click',closeCart);

    // checkout
    const checkoutModal = document.getElementById('checkoutModal');
    document.getElementById('checkoutBtn').addEventListener('click',()=>{
      closeCart();
      checkoutModal.classList.remove('hidden'); checkoutModal.classList.add('flex');
    });
    document.getElementById('closeCheckout').addEventListener('click',()=>{ checkoutModal.classList.add('hidden'); checkoutModal.classList.remove('flex'); });

    // pagamento - toggle boxes
    const payMethod = document.getElementById('payMethod');
    payMethod.addEventListener('change',()=>{
      document.getElementById('pixBox').classList.toggle('hidden', payMethod.value!=='pix');
      document.getElementById('cardBox').classList.toggle('hidden', payMethod.value!=='card');
    });

    // copiar pix
    function copyText(t){ navigator.clipboard.writeText(t).then(()=>alert('Copiado para a área de transferência')) }
    document.getElementById('copyPixBtn').addEventListener('click',()=>copyText(STORE.pixKey));
    document.getElementById('copyPixBtn2').addEventListener('click',()=>copyText(STORE.pixKey));

    // confirmar pagamento (simulado)
    document.getElementById('confirmPayment').addEventListener('click',()=>{
      if(CART.length===0){ alert('Carrinho vazio'); return; }
      const name = document.getElementById('buyerName').value || 'Cliente';
      alert(Pedido confirmado! Obrigado, ${name}.\nVocê será contatado pelo WhatsApp para finalizar.);
      // limpar
      CART = []; updateCartUI(); checkoutModal.classList.add('hidden'); checkoutModal.classList.remove('flex');
    });

    // enviar resumo por whatsapp
    document.getElementById('sendWhats').addEventListener('click',()=>{
      if(CART.length===0){ alert('Carrinho vazio'); return; }
      const name = document.getElementById('buyerName').value || '';
      const addr = document.getElementById('buyerAddr').value || '';
      const total = CART.reduce((s,i)=>s+i.price*i.qty,0).toFixed(2).replace('.',',');
      const lines = CART.map(i=>${i.qty}x ${i.name} - R$ ${formatPrice(i.price*i.qty)});
      const text = Pedido:%0A${lines.join('%0A')}%0A%0ATotal: R$ ${total}%0ANome: ${encodeURIComponent(name)}%0AEndereço: ${encodeURIComponent(addr)};
      const url = https://wa.me/${STORE.whatsapp.replace(/[+\s]/g,'')}?text=${text};
      window.open(url,'_blank');
    });

    // botão de adicionar via buyNow já abre o carrinho
    document.querySelectorAll('.buyNowBtn').forEach(b=>b.addEventListener('click',()=>openCart()));

    // copiar PIX via btn

  </script>

</body>
</html>
