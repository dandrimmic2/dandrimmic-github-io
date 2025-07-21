<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Análise de Viabilidade Fotovoltaica - Sítio São João</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Rural Harmony -->
    <!-- Application Structure Plan: A aplicação foi estruturada como um painel de controle narrativo de cima para baixo. Começa com um resumo executivo (O Problema e A Solução), seguido por uma análise comparativa interativa dos cenários (Off-Grid vs. Híbrido). Em seguida, aprofunda-se na proposta vencedora com gráficos de desempenho e viabilidade. Por fim, apresenta as propostas de planejamento integrado (além da energia) e um plano de ação claro. Essa estrutura foi escolhida para facilitar a rápida compreensão do panorama geral e permitir um aprofundamento progressivo nos detalhes, tornando a exploração mais intuitiva e menos linear que uma apresentação de slides. -->
    <!-- Visualization & Content Choices: 
        - Problema: Informar -> Cards com ícones (Unicode) e estatísticas chave (HTML/CSS) -> Justificativa: Impacto visual rápido.
        - Comparação de Cenários: Comparar -> Botões de alternância (JS) para exibir/ocultar seções de detalhes -> Justificativa: Permite uma comparação direta e focada pelo usuário, muito mais eficaz do que slides sequenciais.
        - Desempenho (Geração vs Consumo): Comparar Mudança -> Gráfico de Barras (Chart.js/Canvas) -> Justificativa: Visualização padrão e eficaz para comparar duas séries de dados ao longo do tempo (meses).
        - Viabilidade Econômica (Payback): Mostrar Mudança -> Gráfico de Linha (Chart.js/Canvas) -> Justificativa: Demonstra claramente a trajetória do investimento ao longo do tempo, destacando o ponto de equilíbrio e o lucro futuro.
        - Planejamento Integrado: Organizar -> Layout de cards em grade (HTML/CSS/Flexbox) -> Justificativa: Apresenta as propostas complementares como pilares de igual importância de forma organizada e visualmente agradável.
        -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8f9fa;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }
        .tab-button.active {
            background-color: #1e3a8a;
            color: #ffffff;
            font-weight: 700;
        }
        .tab-button {
            transition: all 0.3s ease;
        }
    </style>
</head>
<body class="text-gray-800">
    <div class="container mx-auto p-4 md:p-8 max-w-7xl">
        <header class="text-center mb-16">
            <h1 class="text-5xl md:text-6xl font-bold text-blue-900">Energia Fotovoltaica no Sítio São João</h1>
            <p class="mt-4 text-xl text-gray-600">Um estudo de caso sobre autonomia energética, viabilidade econômica e planejamento ambiental rural.</p>
            <p class="text-base text-gray-500 mt-2">Por: Leonardo Mueller Vilela de Carvalho, Matheus Guarnieri Spadaro, Paulo César dos Santos Brugnaro</p>
        </header>
        <section id="desafio" class="mb-16">
            <h2 class="text-4xl font-bold text-center mb-8 text-blue-900">A Realidade Energética do Sítio São João</h2>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
                <div class="text-lg">
                    <p class="text-gray-700 mb-4">
                        A Escola da Floresta, um centro vital de educação ambiental com um histórico de dezenas de milhares de visitantes, enfrenta um paradoxo, no qual promove a sustentabilidade enquanto sofre com uma infraestrutura energética. Localizada no final de uma linha de distribuição da concessionária, a propriedade é afligida por <span class="font-bold">quedas frequentes de energia</span>.
                    </p>
                    <p class="text-gray-700">
                        Essa instabilidade não é um mero inconveniente; ela representa um entrave direto ao funcionamento básico da propriedade e de suas atividades educativas, comprometendo desde a segurança alimentar (refrigeração) até a qualidade da experiência oferecida aos visitantes. A busca por uma solução, portanto, era uma necessidade operacional e uma questão de coerência com a missão da instituição.
                    </p>
                </div>
                <div class="flex justify-center items-center">
                    <img src="https://cdn.pixabay.com/photo/2024/02/24/10/48/solar-panels-8593759_1280.png" alt="Painéis solares instalados no telhado de uma casa rural." class="rounded-lg shadow-md max-w-sm w-full">
                </div>
            </div>
             <div class="grid grid-cols-1 md:grid-cols-3 gap-6 text-center mt-12">
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <span class="text-5xl">⚡</span>
                    <h3 class="font-bold text-2xl mt-4">Instabilidade Crônica</h3>
                    <p class="text-lg text-gray-600 mt-2">Dependência de uma rede de distribuição sobrecarregada e suscetível a falhas.</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <span class="text-5xl">🔌❌</span>
                    <h3 class="font-bold text-2xl mt-4">Falha Operacional</h3>
                    <p class="text-lg text-gray-600 mt-2">Compromete equipamentos essenciais, segurança alimentar e a rotina de todos no local.</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <span class="text-5xl">🎓</span>
                    <h3 class="font-bold text-2xl mt-4">Prejuízo Pedagógico</h3>
                    <p class="text-lg text-gray-600 mt-2">Afeta a qualidade das atividades educativas, o cerne da missão da Escola da Floresta.</p>
                </div>
            </div>
        </section>
        <section id="metodologia" class="mb-16 bg-blue-50 p-8 rounded-lg">
            <h2 class="text-4xl font-bold text-center mb-8 text-blue-900">Nossa Abordagem Metodológica</h2>
            <p class="max-w-4xl mx-auto text-center text-lg text-gray-700 mb-12">
                Este estudo caracteriza-se como um estudo de caso com abordagem quali-quantitativa, estruturado em fases distintas para garantir uma análise completa e sistemática da viabilidade de implementação de um sistema fotovoltaico na Escola da Floresta.
            </p>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h3 class="font-bold text-2xl mb-3"><span class="text-blue-500 font-black">1.</span> Diagnóstico</h3>
                    <p class="text-lg text-gray-600">Coleta de informações essenciais através de um inventário detalhado dos equipamentos elétricos críticos e do consumo energético total (~250 kWh/mês).</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h3 class="font-bold text-2xl mb-3"><span class="text-blue-500 font-black">2.</span> Prospecção</h3>
                    <p class="text-lg text-gray-600">Contato com três empresas especializadas em energia solar para solicitar propostas técnicas e comerciais detalhadas, permitindo a obtenção de orçamentos reais e a comparação de diferentes tecnologias e configurações de sistemas.</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h3 class="font-bold text-2xl mb-3"><span class="text-blue-500 font-black">3.</span> Análise</h3>
                    <p class="text-lg text-gray-600">Análise comparativa dos cenários propostos (Off-Grid vs. Híbrido). A viabilidade econômica foi avaliada pelo cálculo do retorno sobre o investimento (Payback), enquanto a análise ambiental focou nos benefícios da fonte renovável e na gestão do ciclo de vida dos componentes, como a bateria de lítio.</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h3 class="font-bold text-2xl mb-3"><span class="text-blue-500 font-black">4.</span> Proposta</h3>
                    <p class="text-lg text-gray-600">Consolidação de todas as informações em uma proposta técnica final, incluindo especificações dos equipamentos, cronograma financeiro, e recomendações estratégicas para garantir não apenas a autonomia energética, mas também a sustentabilidade e o alinhamento com a vocação pedagógica do local.</p>
                </div>
            </div>
        </section>
        <section id="resultados-diagnostico" class="mb-16">
            <h2 class="text-4xl font-bold text-center mb-8 text-blue-900">Resultados do Diagnóstico: Entendendo a Necessidade</h2>
            <div class="bg-white p-8 rounded-lg shadow-lg">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8 text-lg">
                    <div>
                        <h3 class="font-bold text-2xl mb-3 text-blue-800">Definição do Escopo e Cargas Prioritárias</h3>
                        <p class="text-gray-700 mb-4">O consumo médio mensal da propriedade foi estimado em 250 kWh. No entanto, o ponto crucial definido para o projeto foi que o sistema não precisaria suprir 100% dessa demanda, mas sim garantir o funcionamento de um conjunto de cargas essenciais durante as interrupções. Estas foram definidas como:</p>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>1 Geladeira (segurança alimentar)</li>
                            <li>10 Lâmpadas de LED (iluminação básica)</li>
                            <li>1 Roteador de Internet (comunicação)</li>
                            <li>8 Câmeras de Monitoramento (segurança)</li>
                        </ul>
                    </div>
                    <div>
                        <h3 class="font-bold text-2xl mb-3 text-red-700">Achado Técnico Crítico: A Inviabilidade dos Chuveiros</h3>
                        <p class="text-gray-700">Um consenso unânime entre as 3 empresas consultadas foi a <span class="font-bold">inviabilidade econômica e técnica de alimentar chuveiros elétricos</span> com sistemas baseados em baterias. A altíssima demanda de potência exigiria um banco de baterias e um inversor superdimensionados, elevando o custo do projeto a um patamar impraticável.</p>
                        <p class="text-gray-700 mt-3 font-semibold">A recomendação unânime foi tratar uma demanda térmica (água quente) com uma fonte térmica, ou seja, um sistema de aquecimento solar dedicado (boiler).</p>
                    </div>
                </div>
            </div>
        </section>
        <section id="analise" class="mb-16">
            <h2 class="text-4xl font-bold text-center mb-2 text-blue-900">Análise Comparativa de Cenários</h2>
            <p class="max-w-3xl mx-auto text-center text-lg text-gray-700 mb-8">
                Com base no diagnóstico, duas soluções principais emergiram. Aqui temos uma forma para comparar detalhadamente cada cenário.
            </p>
            <div class="flex justify-center mb-8 rounded-lg p-1 bg-blue-100 max-w-md mx-auto">
                <button id="btn-offgrid" class="tab-button text-lg w-1/2 p-3 rounded-md">Off-Grid (Básico)</button>
                <button id="btn-hibrido" class="tab-button text-lg active w-1/2 p-3 rounded-md">Híbrido (Recomendado)</button>
            </div>
            <div id="content-offgrid" class="hidden">
                <div class="bg-white p-8 rounded-lg shadow-xl border border-gray-200">
                    <h3 class="text-3xl font-bold text-center text-blue-800 mb-6">Cenário 1: Sistema Off-Grid</h3>
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center text-lg">
                        <div>
                            <h4 class="font-bold text-2xl mb-2">Função Principal e Arquitetura</h4>
                            <p class="mb-4">Este sistema opera de forma totalmente independente da rede pública. Sua única função é atuar como um "no-break" robusto, garantindo energia para as cargas essenciais <span class="font-bold">apenas durante as quedas de energia</span>. A energia gerada pelos painéis é armazenada em um banco de baterias e utilizada quando necessário.</p>
                             <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <h5 class="font-bold text-xl mb-1">Investimento</h5>
                                    <p class="text-3xl font-bold text-blue-800">R$ 16.000,00</p>
                                </div>
                                <div>
                                    <h5 class="font-bold text-xl mb-1">Retorno Financeiro</h5>
                                    <p class="text-3xl font-bold text-blue-800">Inexistente</p>
                                </div>
                             </div>
                             <div class="mt-6">
                                <h5 class="font-bold text-2xl mb-2">Vantagens vs. Desvantagens</h5>
                                <ul class="list-disc list-inside text-green-700 mb-3">
                                    <li>Custo inicial 16% menor.</li>
                                    <li>Cumpre o requisito mínimo de autonomia.</li>
                                </ul>
                                <ul class="list-disc list-inside text-red-700">
                                    <li>Não gera economia na fatura de energia.</li>
                                    <li>Benefício restrito aos momentos de queda.</li>
                                </ul>
                            </div>
                        </div>
                        <div class="flex justify-center items-center">
                             <img src="https://wiki.ifsc.edu.br/mediawiki/images/a/a0/Ligsmodulosoff.png" alt="Diagrama de um sistema fotovoltaico off-grid." class="rounded-lg max-w-md w-full bg-white p-2 shadow-lg">
                        </div>
                    </div>
                </div>
            </div>
            <div id="content-hibrido">
                <div class="bg-white p-8 rounded-lg shadow-xl border-2 border-blue-800">
                     <h3 class="text-3xl font-bold text-center text-blue-800 mb-6">Cenário 2: Sistema Híbrido (On-Grid com Backup)</h3>
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center text-lg">
                        <div>
                            <h4 class="font-bold text-2xl mb-2">Função Dupla e Inteligente</h4>
                            <p class="mb-2"><span class="font-bold">1. Modo On-Grid (Operação Diária):</span> O sistema está conectado à rede. Ele gera energia para o consumo da casa e o excedente é injetado na rede da concessionária, gerando créditos que abatem o valor da fatura de energia.</p>
                            <p><span class="font-bold">2. Modo Backup (Queda de Energia):</span> Ao detectar uma falha na rede, o sistema se desconecta automaticamente e a bateria de lítio passa a alimentar as cargas essenciais, garantindo a autonomia.</p>
                             <div class="mt-6">
                                <h5 class="font-bold text-2xl mb-2">Investimento e Retorno</h5>
                                <div class="grid grid-cols-2 gap-4">
                                    <div>
                                        <p class="text-4xl font-bold text-blue-800">R$ 18.556</p>
                                        <p class="text-base text-gray-600">Investimento</p>
                                    </div>
                                    <div>
                                        <p class="text-3xl font-bold text-green-600">6 Anos e 10 meses</p>
                                        <p class="text-base text-gray-600">Payback</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                         <div class="flex justify-center items-center">
                             <img src="https://i0.wp.com/www.ocaenergia.com/wp-content/uploads/2020/08/sistema-hibrido.jpg?resize=616%2C408&ssl=1" alt="Diagrama de um sistema fotovoltaico híbrido." class="rounded-lg max-w-md w-full shadow-lg">
                        </div>
                        <div class="lg:col-span-2">
                            <h4 class="font-bold text-2xl mb-2">Vantagens Estratégicas</h4>
                            <p class="text-gray-700">Esta solução alinha a necessidade de autonomia com a viabilidade econômica. O investimento não é apenas um custo de segurança, mas um ativo que se paga e continua a gerar economia por mais de 25 anos, além de valorizar o imóvel e permitir expansões futuras.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <section id="proposta-detalhada" class="mb-16 bg-blue-50 p-6 md:p-8 rounded-lg">
            <h2 class="text-4xl font-bold text-center mb-2 text-blue-900">Análise Aprofundada da proposta Híbrida</h2>
            <p class="max-w-4xl mx-auto text-center text-lg text-gray-700 mb-8">
                A recomendação central deste estudo é a adoção do Sistema Híbrido. Embora com um investimento inicial 16% superior, suas vantagens a médio e longo prazo o tornam a solução mais racional, estratégica e vantajosa. Abaixo, detalhamos seu desempenho e viabilidade.
            </p>
            <div class="bg-white p-6 rounded-lg shadow-md mb-8">
                <h3 class="text-3xl font-bold mb-4 text-center md:text-left">Especificações Técnicas do Sistema Híbrido</h3>
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-center">
                    <div>
                        <p class="text-base text-gray-500">Potência Instalada</p>
                        <p class="font-bold text-2xl text-blue-800">2,34 kWp</p>
                    </div>
                    <div>
                        <p class="text-base text-gray-500">Painéis Fotovoltaicos</p>
                        <p class="font-bold text-2xl text-blue-800">4x 585W</p>
                    </div>
                    <div>
                        <p class="text-base text-gray-500">Inversor de Tensão</p>
                        <p class="font-bold text-2xl text-blue-800">Híbrido Goodwe 3,5kW</p>
                    </div>
                    <div>
                        <p class="text-base text-gray-500">Armazenamento</p>
                        <p class="font-bold text-2xl text-blue-800">Bateria de Lítio 3,2 kWh</p>
                    </div>
                </div>
            </div>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center text-lg">
                <div>
                    <h3 class="text-3xl font-bold mb-4">Projeção de Desempenho Anual</h3>
                     <p class="text-gray-700 mb-4">
                        O gráfico ilustra a relação entre a energia gerada pelo sistema (azul) e o consumo médio da propriedade (rosa). A geração média mensal de <strong>296 kWh</strong> supera o consumo de <strong>250 kWh</strong>, o que significa que, na maior parte do ano, o sistema produz um excedente de energia. Esse excedente é crucial para o retorno financeiro, pois é convertido em créditos na fatura.
                    </p>
                    <div class="chart-container">
                        <canvas id="generationChart"></canvas>
                    </div>
                </div>
                <div>
                     <h3 class="text-3xl font-bold mb-4">Análise de Viabilidade Econômica</h3>
                      <p class="text-gray-700 mb-4">
                        Este gráfico é a chave para entender a viabilidade do projeto. A linha verde mostra a evolução do valor acumulado. O investimento inicial de R$18.556 é gradualmente recuperado através da economia na conta de luz. O ponto onde a linha cruza o zero, em <span class="font-bold">6 anos e 10 meses</span>, é o payback. A partir daí, o projeto entra em uma fase de lucro líquido, com uma economia total estimada em 20 anos de quase R$40.000.
                    </p>
                    <div class="chart-container">
                        <canvas id="paybackChart"></canvas>
                    </div>
                </div>
            </div>
        </section>
        <section id="planejamento-integrado" class="mb-16">
            <h2 class="text-4xl font-bold text-center mb-8 text-blue-900">Planejamento Ambiental e Pedagógico Integrado</h2>
            <p class="max-w-3xl mx-auto text-center text-lg text-gray-700 mb-12">
                A sustentabilidade do projeto transcende a geração de energia. Uma abordagem holística é fundamental para maximizar os benefícios e alinhar a infraestrutura à missão da Escola da Floresta.
            </p>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="bg-white p-6 rounded-lg shadow-md text-center border-t-4 border-orange-400">
                    <span class="text-5xl">💧</span>
                    <h3 class="font-bold text-2xl my-3">1. Racionalidade Energética</h3>
                    <p class="text-lg text-gray-600">A recomendação para instalar um <span class="font-bold">aquecedor solar térmico</span> é um princípio de eficiência. Tratar uma demanda térmica com uma fonte térmica é energeticamente mais racional e economicamente mais viável, otimizando o investimento no sistema fotovoltaico.</p>
                </div>
                 <div class="bg-white p-6 rounded-lg shadow-md text-center border-t-4 border-green-500">
                    <span class="text-5xl">♻️</span>
                    <h3 class="font-bold text-2xl my-3">2. Sustentabilidade do Ciclo de Vida</h3>
                    <p class="text-lg text-gray-600">A viabilidade ambiental a longo prazo depende da gestão dos componentes. É imprescindível planejar o encaminhamento da bateria de lítio para programas de <span class="font-bold">logística reversa e reciclagem</span> ao fim de sua vida útil, em conformidade com a PNRS (Lei nº 12.305/2010).</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md text-center border-t-4 border-purple-500">
                     <span class="text-5xl">🧑‍🏫</span>
                    <h3 class="font-bold text-2xl my-3">3. Capital Pedagógico</h3>
                    <p class="text-lg text-gray-600">O sistema deve ser um ativo educacional. Propõe-se transformar a infraestrutura em uma <span class="font-bold">ferramenta pedagógica viva</span>, com um tour de energia sustentável e monitores em tempo real para demonstrar na prática os conceitos de energia renovável aos visitantes.</p>
                </div>
            </div>
        </section>
        <section id="implementacao" class="mb-16 bg-gray-100 p-8 rounded-lg">
             <h2 class="text-4xl font-bold text-center mb-8 text-blue-900">Plano de Implementação e Fomento</h2>
             <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 text-center">
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h3 class="font-bold text-2xl mb-3">Orçamento</h3>
                    <p class="text-5xl font-bold text-blue-800">R$ 18.556</p>
                    <p class="text-lg text-gray-600">(Sistema Híbrido) <br>+ Custo do Aquecedor Solar</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h3 class="font-bold text-2xl mb-3">Cronograma</h3>
                    <p class="text-5xl font-bold text-blue-800">1-2</p>
                    <p class="text-lg text-gray-600">Semanas para instalação completa após a contratação da empresa.</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h3 class="font-bold text-2xl mb-3">Linhas de Fomento</h3>
                    <p class="text-3xl font-bold text-green-600">Pronaf Eco</p>
                    <p class="text-lg text-gray-600">Programa Nacional de Fortalecimento da Agricultura Familiar, que oferece crédito com juros subsidiados para projetos de sustentabilidade.</p>
                </div>
             </div>
             <p class="text-center mt-8 text-lg text-gray-700 max-w-4xl mx-auto">A viabilidade do projeto é reforçada pelo ambiente regulatório favorável, como o Marco Legal da Geração Distribuída (Lei nº 14.300/2022), e por programas de financiamento que podem facilitar o acesso ao capital inicial, tornando a proposta não apenas técnica e economicamente sólida, mas também acessível.</p>
        </section>

<section id="aprendizados" class="mb-16">
    <h2 class="text-4xl font-bold text-center mb-8 text-blue-900">Conexão Teoria-Prática: Aprendizados sobre Planejamento Ambiental</h2>
    <div class="bg-white p-8 rounded-lg shadow-lg text-lg">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div>
                <h3 class="font-bold text-2xl mb-3 text-blue-800">A Visão do Rural Contemporâneo</h3>
                <p class="text-gray-700">A disciplina permitiu entender que o rural hoje não pode mais ser visto como um espaço isolado e ultrapassado, e que o rural contemporâneo é dinâmico, multifuncional e em constante transformação. Isso ficou claro tanto nas atividades em sala quanto na prática observada na Escola da Floresta, localizada justamente em uma área que reúne várias das características da franja rural-urbana: uma zona de transição, onde convivem atividades agrícolas, educativas e demandas por serviços urbanos, como energia elétrica estável e internet.</p>
            </div>
            <div>
                <h3 class="font-bold text-2xl mb-3 text-blue-800">Planejamento Integrado na Prática</h3>
                <p class="text-gray-700">A proposta prática de implementar um sistema fotovoltaico no sítio demonstrou como o planejamento ambiental rural deve levar em conta múltiplos fatores, como infraestrutura, usos dos recursos naturais, dinâmica social e acesso a políticas públicas. Em áreas como as franjas rural-urbanas, essas questões se tornam ainda mais complexas, exigindo soluções integradas e sensíveis à realidade local. O trabalho prático reforçou a importância de pensar o rural como espaço de inovação, resiliência e protagonismo no enfrentamento de desafios ambientais e sociais contemporâneos.</p>
            </div>
        </div>
    </div>
</section>
        <footer class="text-center pt-8 border-t">
            <p class="font-bold text-lg">Universidade Federal de São Carlos (UFSCar) - Bacharelado em Gestão e Análise Ambiental</p>
            <p class="text-base text-gray-500 mt-1">Análise realizada como parte das atividades acadêmicas.</p>
        </footer>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const btnOffgrid = document.getElementById('btn-offgrid');
            const btnHibrido = document.getElementById('btn-hibrido');
            const contentOffgrid = document.getElementById('content-offgrid');
            const contentHibrido = document.getElementById('content-hibrido');
            function showTab(tab) {
                if (tab === 'hibrido') {
                    contentHibrido.style.display = 'block';
                    contentOffgrid.style.display = 'none';
                    btnHibrido.classList.add('active');
                    btnOffgrid.classList.remove('active');
                } else {
                    contentHibrido.style.display = 'none';
                    contentOffgrid.style.display = 'block';
                    btnHibrido.classList.remove('active');
                    btnOffgrid.classList.add('active');
                }
            }
            btnHibrido.addEventListener('click', () => showTab('hibrido'));
            btnOffgrid.addEventListener('click', () => showTab('offgrid'));
            showTab('hibrido');
            const generationData = {
                labels: ['Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun', 'Jul', 'Ago', 'Set', 'Out', 'Nov', 'Dez'],
                datasets: [{
                    label: 'Geração (kWh)',
                    data: [322, 340, 296, 275, 234, 217, 229, 283, 290, 324, 331, 352],
                    backgroundColor: 'rgba(29, 78, 216, 0.7)',
                    borderColor: 'rgba(29, 78, 216, 1)',
                    borderWidth: 1
                }, {
                    label: 'Consumo (kWh)',
                    data: [250, 250, 250, 250, 250, 250, 250, 250, 250, 250, 250, 250],
                    backgroundColor: 'rgba(219, 39, 119, 0.6)',
                    borderColor: 'rgba(219, 39, 119, 1)',
                    borderWidth: 1
                }]
            };
            const paybackData = {
                labels: ['Invest.', 'Ano 1', 'Ano 2', 'Ano 3', 'Ano 4', 'Ano 5', 'Ano 6', 'Ano 7', 'Ano 10', 'Ano 20'],
                datasets: [{
                    label: 'Valor Acumulado (R$)',
                    data: [-18556, -15383.62, -12232.09, -9107.76, -6009.91, -2938.54, 106.12, 3124.52, 12022.78, 39975.24],
                    fill: false,
                    borderColor: 'rgb(22, 163, 74)',
                    tension: 0.1,
                    pointBackgroundColor: 'rgb(22, 163, 74)',
                    pointRadius: 5
                },
                {
                    label: 'Ponto de Equilíbrio',
                    data: [0,0,0,0,0,0,0,0,0,0],
                    fill: false,
                    borderColor: 'rgb(200, 200, 200)',
                    borderDash: [5, 5],
                    pointRadius: 0,
                    borderWidth: 2
                }]
            };    
            const chartOptions = (title) => ({
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    title: {
                        display: true,
                        text: title,
                        font: { size: 20 }
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                if (context.parsed.y !== null) {
                                     if (context.dataset.label.includes('Valor')) {
                                        label += new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' }).format(context.parsed.y);
                                     } else {
                                        label += context.parsed.y + ' kWh';
                                     }
                                }
                                return label;
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: false,
                         ticks: {
                            font: {
                                size: 14
                            },
                            callback: function(value, index, values) {
                                if (title.includes('Valor')) {
                                   return 'R$ ' + value.toLocaleString('pt-BR');
                                }
                                return value + ' kWh';
                            }
                        }
                    },
                    x: {
                        ticks: {
                            font: {
                                size: 14
                            }
                        }
                    }
                }
            });
            new Chart(document.getElementById('generationChart'), {
                type: 'bar',
                data: generationData,
                options: chartOptions('Geração vs. Consumo Mensal Estimado')
            });
            new Chart(document.getElementById('paybackChart'), {
                type: 'line',
                data: paybackData,
                options: chartOptions('Projeção de Retorno Financeiro do Sistema Híbrido')
            });
        });
    </script>
</body>
</html>
