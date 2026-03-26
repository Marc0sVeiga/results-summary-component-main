📚 Relatório de Estudo: Componente de Resumo de Resultados
Este documento resume as técnicas de arquitetura CSS e boas práticas de HTML aplicadas no desenvolvimento do desafio do Frontend Mentor.

1. Estrutura e Semântica (HTML5)
Aprendemos que a organização do HTML deve refletir a hierarquia visual do design:

Container Principal: Atua como o "palco" (sumario__container), isolando o componente do restante da página.

Divisão de Blocos: O componente foi dividido em dois grandes grupos: sumario-resultado (esquerda/informativo) e sumario-resumo (direita/detalhado).

2. Arquitetura CSS: O Equilíbrio Híbrido
O maior aprendizado foi como não ser "escravo" de uma única metodologia, buscando a elegância no código:

A. Metodologia BEM (Block Element Modifier)
Usada para estruturar os grandes blocos.

Vantagem: Evita que estilos de um componente "vazem" e quebrem outros elementos do site.

Exemplo: .sumario__container e .sumario-resultado__container.

B. Componentização e Classes Utilitárias
Para os itens que se repetem (Reação, Memória, Verbal e Visual), abandonamos o BEM individual para evitar poluição visual.

Conceito: Criamos a classe .status-item para cuidar de toda a estrutura comum (Flexbox, padding, border-radius).

Vantagem: Escrevemos o código de layout uma única vez, facilitando a manutenção futura.

🎨 CSS Gradientes com Transparência — Aprendizado

Anotação de estudo baseada no desafio Results Summary Component do Frontend Mentor.


🧩 O Problema
Ao replicar um componente de resultado, o círculo central precisava ter um efeito visual de fade: aparecer escuro no topo e ir desaparecendo até se fundir com a cor do container atrás dele.
A tentativa inicial foi inverter as cores do gradiente, mas o efeito correto só é alcançado com transparência no canal alpha.

💡 A Solução — Gradiente com Opacidade
O segredo está em usar hsl() com o quarto parâmetro de alpha, fazendo o elemento ir de semitransparente até totalmente transparente:
css.pontuacao-circulo {
  background: linear-gradient(
    hsl(241, 81%, 54%, 0.5),  /* azul semitransparente no topo */
    hsl(241, 81%, 54%, 0)     /* totalmente transparente na base */
  );
}
Assim, o fundo do container pai "aparece" através do círculo, criando o efeito de fusão visual.

📌 Conceitos Importantes
hsl() vs hsla()
No CSS moderno, não é necessário usar hsla() — o hsl() já aceita o quarto parâmetro de opacidade:
css/* Equivalentes — ambos funcionam */
hsla(241, 81%, 54%, 0.5)
hsl(241, 81%, 54%, 0.5)
Usando variáveis CSS com alpha
Para manter as variáveis do Design Guide, basta criar variações com opacidade no :root:
css:root {
  --grad-azul-royal: hsl(241, 81%, 54%);

  /* Versões com opacidade para efeitos de transparência */
  --grad-azul-royal-50: hsl(241, 81%, 54%, 0.5);
  --grad-azul-royal-0:  hsl(241, 81%, 54%, 0);
}

.pontuacao-circulo {
  background: linear-gradient(
    var(--grad-azul-royal-50),
    var(--grad-azul-royal-0)
  );
}

⚠️ Erro Comum
❌ Abordagem errada✅ Abordagem corretaInverter as cores do gradienteControlar o canal alphalinear-gradient(azul-royal, azul-claro)linear-gradient(hsl(..., 0.5), hsl(..., 0))Muda a tonalidade mas não cria fusãoFunde com o fundo revelando a cor do container

🔑 Resumo Rápido

Gradiente com transparência = canal alpha variando de 0.x até 0
hsl() moderno já suporta alpha — hsla() é legado mas ainda válido
Para fundir um elemento com o fundo, use transparência, não inversão de cor
Crie variantes de variáveis CSS com opacidade para manter o Design Guide organizado