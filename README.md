# 📝 Como usar o script de coletar nomes no Sala do Futuro

## 1. Crie o favorito (bookmarklet)
- Copie o código do script (aquele que começa com `javascript:(function(){...})();`).
- No navegador, adicione um **novo favorito**.
- No campo **URL/endereço**, cole o código inteiro.
- No campo **Nome**, coloque algo como:  
  `📋 Coletar Nomes`

## 2. Acesse sua conta
- Entre normalmente no site do **Sala do Futuro**.
- Faça login com sua conta.

## 3. Navegue até os colegas
- Clique em **Árvore**.  
- Depois vá em **Plantações**.  
- Em seguida, entre em **Colegas**.  
- A lista dos colegas vai aparecer (aquela dentro da caixinha azul).

## 4. Execute o script
- Clique no favorito **📋 Coletar Nomes**.  
- O script vai aguardar **5 segundos**.  
- Nesse tempo, role a lista manualmente para carregar todos os nomes que quiser.

## 5. Coleta final
- Ao terminar os 5 segundos, o script junta todos os nomes carregados.  
- Ele **copia automaticamente** para sua área de transferência (ou mostra uma caixa para copiar manualmente).  
- Agora é só colar a lista no **Word, Excel ou Bloco de Notas**.

---

## 📦 Código do Script

```javascript
javascript:(function(){const DURATION=5;function findContainer(){const sels=['div.Storestyles__ContainerFlat-sc-1tx5gb5-16.crUlEr','div[class*="ContainerFlat"]','div[class*="FlatList"]','div[class*="Storestyles"]'];for(const s of sels){const el=document.querySelector(s);if(el) return el;}const h=Array.from(document.querySelectorAll('h1,h2,h3')).find(x=>x.textContent&&x.textContent.toLowerCase().includes('visite seus amigos'));if(h){if(h.nextElementSibling&&h.nextElementSibling.querySelector&&h.nextElementSibling.querySelector('button'))return h.nextElementSibling;const p=h.parentElement; if(p){const cand=Array.from(p.querySelectorAll('div')).find(d=>d.querySelector&&d.querySelector('button')); if(cand) return cand;}}let best=null,bestCount=0;Array.from(document.querySelectorAll('div')).forEach(d=>{try{const c=d.querySelectorAll?d.querySelectorAll('button').length:0;if(c>bestCount){bestCount=c;best=d;}}catch(e){}});return bestCount>0?best:null;}const container=findContainer();if(!container){alert('❌ Não achei a lista. Abra a lista e tente novamente.');return;}const names=new Set();function safeText(s){return(s||'').replace(/\s+/g,' ').trim();}function addEl(el){try{const n=(el.getAttribute&&el.getAttribute('name'))||el.getAttribute('data-name')||el.textContent||'';const s=safeText(n);if(s)names.add(s);}catch(e){}}function extractFromNode(node){try{if(!node)return;if(node.nodeType===3)return;if(node.querySelectorAll){const nodes=node.querySelectorAll('button[name], [data-name], button, a, span');nodes.forEach(addEl);}else addEl(node);}catch(e){}}extractFromNode(container);const obs=new MutationObserver(muts=>muts.forEach(m=>m.addedNodes.forEach(n=>extractFromNode(n))));obs.observe(container,{childList:true,subtree:true});const overlay=document.createElement('div');overlay.style.cssText='position:fixed;right:12px;bottom:12px;z-index:2147483647;padding:10px 12px;background:#0b74de;color:#fff;border-radius:8px;font-family:sans-serif;font-size:13px;box-shadow:0 4px 14px rgba(0,0,0,.3)';let remaining=DURATION;overlay.innerHTML=`<div id="bm_msg">Role por <b>${remaining}</b>s para carregar mais nomes</div><div style="margin-top:6px;text-align:right"><button id="bm_stop" style="background:#fff;border:none;padding:6px 8px;border-radius:6px;cursor:pointer">Parar</button></div>`;document.body.appendChild(overlay);const msg=overlay.querySelector('#bm_msg');const stopBtn=overlay.querySelector('#bm_stop');const timer=setInterval(()=>{remaining--; if(remaining<=0){clearInterval(timer); finish();}else msg.innerHTML=`Role por <b>${remaining}</b>s para carregar mais nomes`;},1000);function finish(){try{obs.disconnect();}catch(e){}try{overlay.remove();}catch(e){}extractFromNode(container);const final=Array.from(names).filter(Boolean);if(final.length===0){alert('⚠️ Nenhum nome encontrado');return;}const output=final.join('\n');function fallback(){try{const blob=new Blob([output],{type:'text/plain;charset=utf-8'});const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='nomes_chamada.txt';document.body.appendChild(a);a.click();a.remove();setTimeout(()=>URL.revokeObjectURL(a.href),5000);alert('✅ '+final.length+' nomes salvos em nomes_chamada.txt');}catch(e){prompt('Copie os nomes manualmente:',output);}}try{if(navigator.clipboard&&navigator.clipboard.writeText){navigator.clipboard.writeText(output).then(()=>{alert('✅ '+final.length+' nomes copiados para a área de transferência.');}).catch(()=>fallback());}else fallback();}catch(e){fallback();}}stopBtn.addEventListener('click',finish);})();📝 Como usar o script de coletar nomes no Sala do Futuro

1. Crie o favorito (bookmarklet)

Copie o código do script (aquele que começa com javascript:(function(){...})();).

No navegador, adicione um novo favorito.

No campo URL/endereço, cole o código inteiro.

No campo Nome, coloque algo como:
📋 Coletar Nomes.



2. Acesse sua conta

Entre normalmente no site do Sala do Futuro.

Faça login com sua conta.



3. Navegue até os colegas

Clique em Árvore.

Depois vá em Plantações.

Em seguida, entre em Colegas.

A lista dos colegas vai aparecer (aquela dentro da caixinha azul).



4. Execute o script

Clique no favorito 📋 Coletar Nomes.

O script vai aguardar 5 segundos.

Nesse tempo, role a lista manualmente para carregar todos os nomes que quiser.



5. Coleta final

Ao terminar os 5 segundos, o script junta todos os nomes carregados.

Ele copia automaticamente para sua área de transferência (ou mostra uma caixa para você copiar manualmente).

Agora é só colar a lista no Word, Excel ou Bloco de Notas.
