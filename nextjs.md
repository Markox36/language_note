<center><h1>NEXTJS APUNTES</h1></center>

## getServerSideProps

```tsx
export const getServerSideProps: GetServerSideProps = async (context) => {
	const data = await getData();

	// En caso de 404 se pueden retornar opciones predeterminadas por next

	if (!data) {
		// Esta primera forma nos redireccionara a un /404
		return {
			notFound: true,
		};
		// Esta segunda forma nos redireccionara a la ruta que le indiquemos
		return {
			redirect: {
				destination: "/",
				permanent: true, // Cambia codigo de estado de la petición
				statusCode: 303, // Permite modificar el status code al que deseemos
			},
		};
	}

	// Retornar data al componente

	return {
		props: {
			data,
		},
	};
};
```

## getStaticProps

> Tambien conocido como SSG (Static Site Generation) nos permite generar páginas estáticas en tiempo de compilación. Con un HTML y Json predeterminado.

```tsx
export const getStaticProps: GetStaticProps = async (context) => {
	const data = await getData();

	// Retornar data al componente

	return {
		props: {
			data,
		},
	};
};
```

## getStaticPaths

> Podria ocurrir que necesitemos generar multiples páginas estáticas, para ello podemos usar getStaticPaths. Este método nos permite generar multiples páginas estáticas en tiempo de compilación.

```tsx
export const getStaticPaths: GetStaticPaths = async () => {
	const paths = await getPaths();

	return {
		paths,
		fallback: true, // Indica si se debe generar una página estática en tiempo de ejecución
	};
};
```
