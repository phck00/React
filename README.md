# React
const { exec } = require('child_process');
const path = require('path');
const fs = require('fs');

// Função para criar e iniciar um projeto React
const criarProjetoReact = () => {
    const nomeProjeto = 'meu-projeto-react';
    
    // Criar um novo projeto React
    exec(`npx create-react-app ${nomeProjeto}`, (error, stdout, stderr) => {
        if (error) {
            console.error(`Erro ao criar o projeto React: ${error}`);
            return;
        }
        console.log(`Projeto React "${nomeProjeto}" criado com sucesso!`);
        
        // Navegar para o diretório do projeto
        const diretorioProjeto = path.join(__dirname, nomeProjeto);
        process.chdir(diretorioProjeto);
        
        // Instalar dependências adicionais (Bootstrap neste exemplo)
        exec('npm install bootstrap', (error, stdout, stderr) => {
            if (error) {
                console.error(`Erro ao instalar as dependências adicionais: ${error}`);
                return;
            }
            console.log('Dependências adicionais instaladas com sucesso!');
            
            // Escrever importação do Bootstrap no arquivo App.js
            const arquivoApp = path.join(diretorioProjeto, 'src', 'App.js');
            fs.appendFile(arquivoApp, '\nimport \'bootstrap/dist/css/bootstrap.min.css\';\n', (err) => {
                if (err) {
                    console.error(`Erro ao escrever a importação do Bootstrap: ${err}`);
                    return;
                }
                console.log('Importação do Bootstrap adicionada ao arquivo App.js com sucesso!');
                
                // Iniciar o servidor de desenvolvimento
                console.log('Iniciando o servidor de desenvolvimento...');
                exec('npm start');
            });
        });
    });
};

// Chamando a função para criar e iniciar o projeto React
criarProjetoReact();
