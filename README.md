    class CaixaDaLanchonete {
        constructor() {
            this.cardapio = {
                cafe: { descricao: 'Café', valor: 3.00 },
                chantily: { descricao: 'Chantily (extra do Café)', valor: 1.50 },
                suco: { descricao: 'Suco Natural', valor: 6.20 },
                sanduiche: { descricao: 'Sanduíche', valor: 6.50 },
                queijo: { descricao: 'Queijo (extra do Sanduíche)', valor: 2.00 },
                salgado: { descricao: 'Salgado', valor: 7.25 },
                combo1: { descricao: '1 Suco e 1 Sanduíche', valor: 9.50 },
                combo2: { descricao: '1 Café e 1 Sanduíche', valor: 7.50 }
            };
            this.formasDePagamento = ['dinheiro', 'debito', 'credito'];
        }
        calcularValorDaCompra(formaDePagamento, itens) {
            if (!this.formasDePagamento.includes(formaDePagamento)) {
                return "Forma de pagamento inválida!";
            }
        
            if (itens.length === 0) {
                return "Não há itens no carrinho de compra!";
            }
        
            let total = 0;
            let itemsMap = {};
            let hasCafe = false;
            let hasSanduiche = false;
        
            for (const item of itens) {
                const [codigo, quantidade] = item.split(',');
                const menuItem = this.cardapio[codigo];
        
                if (!menuItem) {
                    return "Item inválido!";
                }
        
                if (quantidade <= 0) {
                    return "Quantidade inválida!";
                }
        
                if (codigo === 'cafe') {
                    hasCafe = true;
                }
        
                if (codigo === 'sanduiche') {
                hasSanduiche = true;
            }
    
            if (codigo === 'chantily' && !hasCafe) {
                return "Item extra não pode ser pedido sem o principal";
            }
    
            if (codigo === 'queijo' && !hasSanduiche) {
                return "Item extra não pode ser pedido sem o principal";
            }
    
            if (!itemsMap[codigo]) {
                itemsMap[codigo] = { quantidade: 0, valor: menuItem.valor };
            }
    
            itemsMap[codigo].quantidade += parseInt(quantidade);
        }
    
        for (const codigo in itemsMap) {
            const item = itemsMap[codigo];
            total += item.valor * item.quantidade;
        }
    
        if (formaDePagamento === 'dinheiro') {
            total *= 0.95; // 5% de desconto
        } else if (formaDePagamento === 'credito') {
            total *= 1.03; // 3% de acréscimo
        }
    
        return `R$ ${total.toFixed(2)}`;
        }
    }
