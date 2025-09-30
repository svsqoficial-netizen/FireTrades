# FireTrades
Firetrades a melhor loja de contas e de brainrots etc:
*/
</div>
</div>
</aside>
</main>


{/* Modal de visualização */}
{selected && (
<div className="fixed inset-0 bg-black/40 flex items-center justify-center p-4">
<div className="bg-white rounded max-w-xl w-full p-4">
<div className="flex justify-between items-start">
<div>
<h3 className="text-lg font-semibold">{selected.title} <span className="text-xs text-gray-400">({selected.id})</span></h3>
<p className="text-sm text-gray-600">R$ {selected.priceBRL.toFixed(2)} • {selected.rarity}</p>
<p className="mt-2 text-sm">{selected.description}</p>
</div>
<div className="flex flex-col gap-2">
<button onClick={() => addToCart(selected)} className="px-3 py-1 rounded bg-blue-600 text-white">Adicionar ao carrinho</button>
<button onClick={() => setSelected(null)} className="px-3 py-1 rounded border">Fechar</button>
</div>
</div>
</div>
</div>
)}


{/* Painel Admin simples */}
{showAdmin && (
<div className="fixed right-6 bottom-6 bg-white border rounded p-4 w-80 shadow-lg">
<h3 className="font-semibold">Painel Admin (protótipo)</h3>
<AddAccountForm onAdd={addAccount} />
<div className="mt-3 text-xs">
<p>Contas totais: {accounts.length}</p>
<p>Vendidas: {accounts.filter(a => a.sold).length}</p>
</div>
</div>
)}


<footer className="max-w-5xl mx-auto mt-8 text-xs text-gray-500">
<p>Prototipo criado para demonstração — implemente backend, segurança e meios de pagamento antes de colocar em produção.</p>
</footer>
</div>
);
}


function AddAccountForm({ onAdd }) {
const [id, setId] = useState('');
const [title, setTitle] = useState('');
const [price, setPrice] = useState('');
const [rarity, setRarity] = useState('Comum');
const [desc, setDesc] = useState('');


function submit(e) {
e.preventDefault();
if (!id || !title || !price) { alert('Preencha id, título e preço'); return; }
onAdd({ id, title, priceBRL: parseFloat(price), rarity, description: desc, sold: false });
setId(''); setTitle(''); setPrice(''); setDesc('');
}


return (
<form onSubmit={submit} className="mt-3">
<input value={id} onChange={e=>setId(e.target.value)} placeholder="ID (ex: BFX-010)" className="w-full p-1 border rounded text-xs mb-1" />
<input value={title} onChange={e=>setTitle(e.target.value)} placeholder="Título" className="w-full p-1 border rounded text-xs mb-1" />
<input value={price} onChange={e=>setPrice(e.target.value)} placeholder="Preço (R$)" className="w-full p-1 border rounded text-xs mb-1" />
<select value={rarity} onChange={e=>setRarity(e.target.value)} className="w-full p-1 border rounded text-xs mb-1">
<option>Comum</option>
<option>Top</option>
<option>Lendário</option>
</select>
<textarea value={desc} onChange={e=>setDesc(e.target.value)} placeholder="Descrição" className="w-full p-1 border rounded text-xs mb-1" />
<button className="w-full p-2 rounded bg-indigo-600 text-white text-sm">Adicionar conta</button>
</form>
);
}
