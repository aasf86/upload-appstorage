# upload-appstorage

Local demo

```cmd
git clone https://github.com/aasf86/upload-appstorage
npm install
cd upload-appstorage\
npm start
```


```js
function uploadFile (file) {
	return new Promise( (resolve, reject) => {
		const xhr = new XMLHttpRequest();
		let baseUrl = 'http://<domain>/upload/';
		let urlFinal = baseUrl + Math.random().toString().replace('.', '')+'/'+ file.name;

		console.log('urlFinal', urlFinal);

		let fd = new FormData();
		// adicione ao fd as demais informações que você pretende enviar por POST
		// ao servidor, além do(s) arquivo(s)
	
		// agora é hora de adicionarmos o(s) arquivo(s)
		fd.append('body', file) // nome para referência ao arquivo no formulário
		fd.append('url', urlFinal) // nome para referência ao arquivo no formulário
		xhr.open('post', urlFinal) // path da rota no servidor

		xhr.onerror = reject // em caso de erro, rejeitamos a promise
		xhr.onload = event => {
			// o envio ocorreu com sucesso
			resolve(); // resolvemos nossa promise
		}

		if (xhr.upload) {
			// caso tenhamos acesso a esta informação
			xhr.upload.onprogress = progress => {
				console.log(Math.round((progress.loaded * 100) / progress.total) + '%')
			}
		} 
		else {
		// tratamento em navegadores que não suportam xhr.upload
		}

		xhr.send(fd) // iniciando a requisição, enviando o FormData
	});      
}  

function onSubmit(){
	event.preventDefault()
	var inputFile = document.querySelector('input[type="file"]');
	debugger;
	console.log('vai');
	uploadFile(inputFile.files[0])
	.then(function (response){
		console.log('response', response);
		//response.json();                    
	})
	.then(function(json){
		console.log('json', json);
	})
	.catch(function(error){
		console.log('error', error);
	});

}
```		

```html
<body>
	<input name="arquivo" type="file" />
	<button onclick="onSubmit()">Enviar</button>
</body>
```

Creditos
-----

FELIPE N. MOURA.

[`Fazendo upload com controle de progresso com JavaScript`]: (https://braziljs.org/blog/fazendo-upload-com-controle-de-progresso-com-javascript/) ...

