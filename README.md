# Desafio "Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados"

##### Como parte da resolução do desafio proposto pela DIO, será descrito neste documento as etapas de como foi realizado o uso da ferramenta Azure AI Search para pesquisa cognitiva.

##### Os passos seguidos foram:

###### 1. Foi criada uma conta no Portal do Azure (https://portal.azure.com/).
###### 2. Após a conta criada, foi realizada a criação do Resource Group.
###### 3. Com o Resource Group criado, foi realizada a criação de um Azure AI Services, com as seguintes configurações:

    Subscription: Your Azure subscription.
    Resource group: LAB-AI-900-DIO
    Region: East US.
    Name: idiomaLanguageDIO.
    
###### 4. Para prosseguir com o laboratório, também foi realizada a criação de um Recurso do Azure AI Search, com as seguintes configurações: 

    Subscription: Your Azure subscription.
    Resource group: LAB-AI-900-DIO
    Region: East US.
    Name: labazureaisearchdio.

###### 5. Como forma de prosseguir com o desafio, foi também criada uma Storage Account, para poder receber os arquivos para a análise, segue abaixo a configuração:

    Subscription: Your Azure subscription.
    Resource group: LAB-AI-900-DIO
    Region: East US.
    Storage account name: storagelaboratoriodio.
    Location: East US.
    Performance: Standard
    Redundancy: Locally redundant storage (LRS)
    
###### 6. Com a Storage Account criada, foi realizada a criação de um Container, com as seguintes informações:

    Name: coffee-reviews
    Public access level: Container (anonymous read access for containers and blobs)
    Advanced: no changes.
    
###### 7. Como solicitado para o laboratório, foi realizado o download do arquivo .zip encontrado no Link "https://aka.ms/mslearn-coffee-reviews", realizada a extração e feito o upload para o container "coffee-reviews".

###### 8. Após upload dos arquivos, utilizando a ferramenta Azure Ai Search, foi realizado a indexação dos arquivos, fazendo a importação para a ferramenta.

###### 9. Após o upload, foi realizada a configuração do Azure Blob Storage, do Indexador, e também realizada a configuraçào dos parâmetros de análise, conforme detalhes abaixo:

    On the Connect to your data page, in the Data Source list, select Azure Blob Storage. Complete the data store details with the following values:
        Data Source: Azure Blob Storage
        Data source name: coffee-customer-data
        Data to extract: Content and metadata
        Parsing mode: Default
        Connection string: *Select Choose an existing connection. Select your storage account, select the "coffee-reviews" container, and then click Select.
        Managed identity authentication: None
        Container name: this setting is auto-populated after you choose an existing connection.
        Blob folder: Leave this blank.
        Description: Reviews for Fourth Coffee shops.
        Select Next: Add cognitive skills (Optional).
    
    In the Attach Cognitive Services section, select your Azure AI services resource.
    
    In the Add enrichments section:
        Change the Skillset name to coffee-skillset.
        Select the checkbox Enable OCR and merge all text into merged_content field.
        Ensure that the Source data field is set to merged_content.
        Change the Enrichment granularity level to Pages (5000 character chunks).
        Don’t select Enable incremental enrichment
        
        Select the following enriched fields:
            Cognitive Skill	Parameter	Field name
            Extract location names	 	locations
            Extract key phrases	 	keyphrases
            Detect sentiment	 	sentiment
            Generate tags from images	 	imageTags
            Generate captions from images	 	imageCaption
            Under Save enrichments to a knowledge store, select:
            Image projections
            Documents
            Pages
            Key phrases
            Entities
            Image details
            Image references
            
    Note If a warning asking for a Storage Account Connection String appears.
    
    Select Choose an existing connection. Choose the storage account you created earlier.
    Click on + Container to create a new container called "knowledge-store" with the privacy level set to Private, and select Create.
    Select the "knowledge-store" container, and then click Select at the bottom of the screen.
    Select Azure blob projections: Document. A setting for Container name with the knowledge-store container auto-populated displays. Don’t change the container name.
    
    Select Next: Customize target index. Change the Index name to "coffee-index".
    
    Ensure that the Key is set to metadata_storage_path. Leave Suggester name blank and Search mode autopopulated.
    Review the index fields’ default settings. Select filterable for all the fields that are already selected by default.
    
    Screenshot that shows the customize index pane with the index name entered and 'Filterable' selected for a default index field.
    
    Select Next: Create an indexer.
    Change the Indexer name to coffee-indexer.
    Leave the Schedule set to Once.
    
    Expand the Advanced options. Ensure that the Base-64 Encode Keys option is selected, as encoding keys can make the index more efficient.
    
    Select Submit to create the data source, skillset, index, and indexer. The indexer is run automatically and runs the indexing pipeline, which:
    Extracts the document metadata fields and content from the data source.
    Runs the skillset of cognitive skills to generate more enriched fields.
    Maps the extracted fields to the index.
    
    
    
###### 10. Configurações realizadas, no Azure AI Search, na aba "Overview", clickamos em "Search Explorer". Em index, colocamos o indexador que criamos, o "coffee-index". Logo após, foi realizada duas pesquisas: A primeira, utilizando o comando "search=locations:'Chicago'" que nos trouxe todos os formulários que foram preenchidos, sinalizando que foram da cidade "Chicago". Logo após, foi usado o comando "search=sentiment:'negative'", aonde nos mostrou os comentarios que estavam descontentes com a experiência que teve no ambiente. O mesmo nos retornou um comentário negativo, aonde o mesmo foi feito devido a demora no serviço.

###### 11. A lição que eu posso tirar, ao usar as ferramentas do Azure em questão, é que podemos usar elas para elaborar estratégias de mercado, resolução de falhas de atendimento, estudos de caso, entre várias outros casos que podemos usar para otimização de nossos trabalhos, através de dados extraidos do público-alvo de nossos afazeres.

###### 12. Após o término nas análises, foi realizada a remoção da Workspace e do Resource Group, para evitar gastos excedentes.
