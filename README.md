<!DOCTYPE html>
<html lang="en">
<head>

    <!-- JS -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
    <!-- Gráficos --> <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Open+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;0,800;1,300;1,400;1,500;1,600;1,700;1,800&display=swap" rel="stylesheet">

    <style>
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: 'Open Sans', 'Arial';
}

/* Variáveis de Cores */
:root {
    --cor-principal: #061e4e;
    --cor-destaque: #3498db;
}

/* Gráfico de rosca */
.grafico-rosca{
    height: 60px;
    width: 60px;
}


/* Sessão */
section.formacao{
    padding: 10px;
}
section.formacao article h3{
    margin-bottom: 20px;
    font-size: 25px;
    text-transform: uppercase;
    color: #061e4e;
}   

section.formacao article > div {
	margin: 25px 0;
}

section.formacao article div h4 {
	font-weight: 400;
	font-size: 22px;
	margin: 5px 0;
	color: #061e4e;
}
.formacao article.programacao{
    display: grid;
    column-gap: 50px;
    grid-template-columns: repeat(2, 1fr);
    grid-template-areas:
        "a a"
        "b c";
}
.formacao article.programacao h3{
    grid-area: a;
    text-align: center;
}
.formacao article.programacao h3 span{
    padding: 10px 20px;
    z-index: 10;
    position: relative;
    background-color: #f7f7f7;
}
.formacao header{
    margin-bottom: 20px;
    display: flex;
    flex-direction: row;
    align-items: center;
}
.formacao article .linguagem-programacao {
    padding: 30px;
    background-color: rgba(250, 250, 250, 0.6);
    border: 1px solid #d9d9d9;
    /* border-radius: 15px; */
    max-width: 90vw;
}
.formacao header .titulo{
    margin-left: 20px;
}
.formacao header h4{
    margin: 0;
}
.formacao header h5{
    font-size: 0.8em;
    margin-top: -10px;
}
.formacao p{
    text-align: justify;
}

    </style>
</head>
<body>
    
<section id="formacao" class="formacao">

    <article class="programacao">
        
        <!-- Cards adicionados com o JavaScript -->

    </article><!-- programacao -->

</section>




    <script>

// Linguagens de Programação
const linguagensProgramacao = [
    {
        nome: "HTML e CSS",
        nivel: "Intermediário/Avançado",
        percetual: 75,
        descricao: "Semântica, formulários avançados, meta tags SEO, Seletores Avançados, Unidades de Medida Avançadas, Flexbox e Grid Layout, Media Queries, Posicionamento, Transições e Animações."
    },
    {
        nome: "PHP",
        nivel: "Intermediário",
        percetual: 60,
        descricao: "Arrays, operações matemáticas, funções, loops, funções nativas, banco de dados, manipulação de arquivos."
    },
    {
        nome: "JavaScript",
        nivel: "Intermediário",
        percetual: 60,
        descricao: "Variáveis, condições, funções, loops, arrays, objetos, classes, operações matemáticas, DOM e manipulação de eventos."
    },
    {
        nome: "JQuery",
        nivel: "Intermediário/Avançado",
        percetual: 75,
        descricao: "DOM, estilização, animações, eventos e interatividade."
    },
    {
        nome: "Python",
        nivel: "Iniciante",
        percetual: 30,
        descricao: "Arrays, operadores aritméticos, de comparação, lógicas, condicionais, saída de dados, loops, funções."
    },
    {
        nome: "Excel",
        nivel: "Intermediário/Avançado",
        percetual: 75,
        descricao: "Funções lógicas, avançadas e de texto, análise de dados, gráficos avançados, formatação de células, tabelas, dashboards e automatização com macros."
    }
]

var programacaoArticle = $('#formacao .programacao');
const graficos = [];
const data = [];

linguagensProgramacao.forEach((nome, index)=>{
    programacaoArticle.append(`
    
    <div class="linguagem-programacao">
        <div class="titulo">
            <header>
                <div class="grafico-rosca">
                    <canvas id="grafico-${index}"></canvas>
                </div>
                <!-- Gráfico rosca -->
                
                <div class="titulo">
                    <h4>${linguagensProgramacao[index]["nome"]}</h4>
                    <h5>${linguagensProgramacao[index]["nivel"]}</h5>
                </div>
                <!-- /.titulo -->
            </header>
        </div>
        <!-- /.titulo -->
        <p>
            ${linguagensProgramacao[index]["descricao"]}
        </p>
    </div>
    <!-- linguagem-programacao -->

    `);

    // Criando uma lista 'graficos' para colocar os objetos (canvas) dos gráficos que serão colocados na página
    graficos.push(document.getElementById('grafico-'+index).getContext('2d'));
    // Aqui estou criando uma lista 'data' com objetos com as informações dos percentuais e das cores dos gráficos
    data.push({
        datasets: [{
          data: [linguagensProgramacao[index]["percetual"], 100-linguagensProgramacao[index]["percetual"]],
          backgroundColor: ['#061e4e', '#d8d8d8']
        }]
    });
})



// Configurar gráfico doughnut
const options = {
  responsive: true,
  maintainAspectRatio: false,
  legend: {
    display: false // Desativa a exibição da legenda
  }
};

// Gerar gráficos
graficos.forEach((item, indice) => {
    var item = new Chart(graficos[indice], { // Aqui é onde informa o objeto canvas que irá ser colocado o gráfico. Estou puxando as informações do array 'graficos' criado dentro do forEach acima
        type: 'doughnut',
        data: data[indice], // Aqui é onde informa o percentual e as cores que irá colocar no gráfico no formato do comentário abaixo. Estou puxando as informações do array 'data' criado dentro do forEach acima
        /*
            data: {
                datasets: [{
                data: [linguagensProgramacao[index]["percetual"], 100-linguagensProgramacao[index]["percetual"]],
                backgroundColor: ['#061e4e', '#d8d8d8']
                }]
            },
        */
        options: options
      });
});
    </script>
</body>
</html>
