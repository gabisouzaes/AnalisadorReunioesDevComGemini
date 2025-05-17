# AnalisadorReunioesDevComGemini: Insights de Reuniões 1:1 com IA

Este projeto apresenta uma ferramenta Python, desenvolvida para Google Colab, que automatiza a análise de anotações de reuniões 1:1 de desenvolvimento. Utilizando as APIs do Google Docs e do Google Gemini, a solução extrai percepções valiosas para apoiar o crescimento profissional e técnico dos liderados pela líder técnica Gabriella.

## 🎯 Qual Problema Resolvemos?

Analisar manualmente múltiplas anotações de reuniões para identificar padrões de desenvolvimento, progressos e desafios pode ser um processo demorado e subjetivo. Esta ferramenta visa:

* **Agilizar a Análise:** Reduzir significativamente o tempo gasto na revisão de transcrições.
* **Extrair Insights Acionáveis:** Transformar o conteúdo bruto das reuniões em informações concisas sobre focos de desenvolvimento, progressos, obstáculos e recomendações.
* **Apoiar o Desenvolvimento Contínuo:** Fornecer uma base de dados para o acompanhamento da evolução dos liderados e para a tomada de decisões mais informada pela liderança.

## ✨ Funcionalidades

* **Leitura de Google Docs:** Coleta IDs de documentos do Google Docs fornecidos pelo usuário.
* **Integração com Google Gemini:** Envia o conteúdo textual combinado das reuniões para análise pela IA do Gemini.
* **Análise Agrupada:** Interpreta o conjunto de anotações como um todo para um liderado específico, identificando tendências ao longo do tempo.
* **Geração de Percepções de Desenvolvimento:** Com base em um prompt customizado, a IA produz um resumo textual destacando:
    * Áreas de foco (técnicas e comportamentais).
    * Evidências de progresso ou estagnação.
    * Desafios recorrentes.
    * Recomendações de próximos passos.
* **Ambiente Colab:** Otimizado para execução em Google Colab.

## 🛠️ Stack Tecnológico

* **Linguagem:** Python 3
* **Ambiente Principal:** Google Colab
* **APIs Google:**
    * Google Gemini API (via `google-generativeai`)
    * Google Docs API (via `google-api-python-client`)
* **Principais Bibliotecas Python:**
    * `os`
    * `json`
    * `google-colab` (para `userdata` e `auth`)
    * `google-api-python-client`
    * `google-auth-httplib2`, `google-auth-oauthlib`
    * `IPython` (para `display` e `Markdown`)

## ⚙️ Configuração do Ambiente

Para executar este projeto, siga os passos abaixo:

1.  **Google Colab:** Abra o notebook (`.ipynb`) no Google Colab.
2.  **Chave da API Google Gemini:**
    * Crie uma chave de API no [Google AI Studio](https://aistudio.google.com/app/apikey).
    * No Colab, vá em "Secrets" (ícone de chave na barra lateral esquerda) e adicione um novo segredo com o nome `GOOGLE_API_KEY` e cole sua chave como valor.
3.  **API do Google Docs:**
    * Verifique se a API do Google Docs está habilitada no seu [Console do Google Cloud](https://console.cloud.google.com/apis/library/docs.googleapis.com).
4.  **Autenticação no Colab:**
    * Ao executar o script pela primeira vez, o Colab solicitará permissão para acessar seus arquivos do Google Docs. Siga as instruções do pop-up para autenticar sua conta Google.

## 🚀 Guia de Uso Rápido
Para utilizar a ferramenta, execute as células do notebook Google Colab na ordem em que aparecem. As principais etapas são:

1.  **Instalação de Dependências e Importações:** As primeiras células cuidam da instalação das bibliotecas Python necessárias e das importações de módulos.
2.  **Configuração Inicial:**
    * Certifique-se de que sua `GOOGLE_API_KEY` foi carregada corretamente a partir dos Secrets do Colab.
    * Verifique se a variável `TECH_LEAD_NAME` está definida como "Gabriella".
    * Confirme o nome do modelo Gemini a ser usado (ex: `NOME_MODELO_GEMINI_STRING = "gemini-1.5-flash-latest"`).
3.  **Inicialização dos Serviços:**
    * O script irá autenticar seu acesso ao Google Docs (você precisará aprovar no pop-up) e inicializar o objeto do modelo Gemini. Monitore as mensagens de saída para confirmar o sucesso.
4.  **Definição das Funções e Prompt:** As funções auxiliares para leitura de documentos, coleta de IDs e a variável com o prompt de análise (`PROMPT_INSIGHTS`) serão definidas.
5.  **Execução da Análise:**
    * **Coleta de IDs:** Você será solicitado(a) a inserir os IDs dos Google Docs que contêm as anotações das reuniões.
        * **Importante:** Forneça apenas o **ID do documento**, não o link completo. O ID é a longa sequência de caracteres na URL do Google Docs, geralmente entre `/d/` e `/edit`.
        * Digite "fim" ou pressione Enter em uma linha vazia (após adicionar pelo menos um ID) para concluir a coleta.
    * **Geração de Insights:** Após fornecer os IDs, o script lerá os documentos, combinará os textos e os enviará ao Gemini para análise com base no prompt definido.
    * **Resultado:** Os insights gerados pela IA serão exibidos na saída da célula.

**Nota sobre Privacidade e Exemplos:**
Para preservar a identidade das pessoas e a confidencialidade do conteúdo técnico discutido nas reuniões 1:1 reais, o nome do "liderado" foi generalizado nas discussões e nos exemplos. Para facilitar os testes e demonstrar o funcionamento da ferramenta, disponibilizamos simulações de anotações de 1:1. Estas anotações são baseadas em cenários reais, mas foram adaptadas para serem genéricas.

* **Acesse os exemplos de anotações aqui:** `(https://drive.google.com/drive/folders/1Z4A8K_9qjmarNMOiQHyZDl7-Wi55vsd-?usp=drive_link)` 

O código foi projetado para funcionar com outros arquivos de anotações, desde que o formato de entrada (ID do Google Docs) seja respeitado.

## 📝 Prompt Base para Análise com Gemini

O modelo Gemini é instruído com o seguinte prompt para realizar a análise:
```text
Você é uma assistente de IA com especialidade em identificar tendências de desenvolvimento em séries de conversas 1:1.
As reuniões analisadas são entre {nome_da_lider} (líder técnica) e um de seus liderados.
Interprete o conjunto de anotações de reuniões fornecido abaixo como um todo, refletindo a jornada de desenvolvimento deste liderado específico com {nome_da_lider}.

Com base em todas as anotações fornecidas, elabore um resumo com suas percepções gerais sobre os pontos de desenvolvimento do liderado. Em seu resumo, procure destacar:

* As principais áreas de foco para desenvolvimento (técnicas e comportamentais) que se mantiveram ao longo do tempo.
* Evidências claras de progresso ou, alternativamente, áreas onde o desenvolvimento pareceu estagnado ou enfrentou dificuldades.
* Desafios ou obstáculos que foram mencionados ou observados de forma recorrente.
* De 1 a 3 recomendações principais ou próximos passos para o desenvolvimento futuro do liderado.

Apresente suas percepções de forma clara, direta e concisa.
