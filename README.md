Onde você está?

Projeto em duas partes:

Coleta: uma página web de arquivo único (HTML, CSS e JS) que registra o nome de um local e suas coordenadas em um Google Forms.
Análise: um script em Python que lê esses registros da planilha do formulário e consulta a temperatura atual de cada local na API Open-Meteo.

A página roda no GitHub Pages, sem build e sem dependências.

Estrutura
Arquivo	Função
index.html	Página de coleta (local, latitude e longitude)
clima.py	Lê a planilha e consulta a temperatura de cada local
Parte 1: página de coleta
Funcionalidades
Captura de latitude e longitude pelo GPS do aparelho, com a precisão em metros.
Preenchimento manual das coordenadas (aceita ponto ou vírgula).
Validação dos campos antes do envio.
Envio para o Google Forms sem sair da página.
Link de reserva que abre o formulário original já preenchido.
Layout responsivo, em tema escuro (preto, cinza e roxo).
Como funciona

A página envia um POST para o endpoint formResponse do Google Forms:

Campo	ID do campo
Nome do local	entry.1262610957
Latitude	entry.41240879
Longitude	entry.287518464

O envio usa mode: "no-cors", porque o Google não libera CORS. A página não consegue ler a resposta: se não houver erro de rede, ela considera o registro enviado. Confira as respostas na planilha.

Publicar no GitHub Pages
Coloque o index.html na raiz do repositório.
Vá em Settings → Pages.
Em Source, escolha a branch (por exemplo main) e a pasta / (root).
Acesse https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/.
Personalizar
Cores e fontes: bloco PERSONALIZE AQUI no início do <style>.
Seu nome e frase: objeto PERFIL no início do <script>.
Outro formulário: troque FORM_URL e os IDs em ENTRY no <script>. Para achar os IDs, use Obter link pré-preenchido no formulário e leia os parâmetros entry.XXXXXXX.
Parte 2: consulta de clima com Python

O clima.py faz este fluxo:

Lê a planilha de respostas do formulário (exportada como CSV) com pandas.
Para cada linha, chama a API Open-Meteo com a latitude e a longitude do local.
Mostra uma tabela com nome, coordenadas, temperatura atual (°C) e horário da medição.
Executar
bash
pip install pandas requests
python clima.py

No Google Colab ou em Jupyter, o código também roda em células; troque print(...) por display(...) se quiser a tabela formatada.

Requisitos
A planilha precisa estar compartilhada como "Qualquer pessoa com o link pode ver", senão o download do CSV falha.
Os cabeçalhos das colunas devem ser exatamente Nome do local, Latitude e Longitude, os mesmos nomes das perguntas do formulário.
Para usar outra planilha, troque SHEET_URL no topo do script.
A Open-Meteo não exige chave de API para uso não comercial.
Observações
A geolocalização só funciona em HTTPS (o GitHub Pages já usa) ou em localhost, e o navegador pede permissão na primeira vez.
Formulários com login obrigatório ou limite de uma resposta por pessoa podem recusar o envio direto.
As fontes vêm do Google Fonts; sem conexão, a página usa as fontes do sistema.
