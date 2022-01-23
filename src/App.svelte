<script>
  let products = [
    {
      id: 1,
      name: "HP Probook",
      description: "HP Laptop i5core",
      category: "Laptop",
      imageURL:
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcToHsQnBXzQ-ebndyEC4CnQZfhPgVNy_XsbyQ&usqp=CAU",
    },
    {
      id: 2,
      name: "AMD GamerReady",
      description: "PC Gaming descktop",
      category: "Desktop",
      imageURL:
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXBUn6iqLTIcnB5EhyWnPZq_-uHF9dY9Xg2w&usqp=CAU",
    },
    {
      id: 3,
      name: "you Product",
      description: "Here is the description",
      category: "Other",
      imageURL: "",
    },
  ];

  let product = {
    id: "",
    name: "",
    description: "",
    category: "",
    imageURL: "",
  };

  let editStatus = false;

  const addProduct = () => {
    // Adding a new Product
    const newProd = {
      id: products.length + 1,
      name: product.name,
      description: product.description,
      category: product.category,
      imageURL: product.imageURL,
    };

    products = products.concat(newProd);
    clearProd();
    editStatus == false;
  };

  const updateProd = () => {
    let updateProduct = {
      id: products.id,
      name: product.name,
      description: product.description,
      category: product.category,
      imageURL: product.imageURL,
    };

    const prodIndex = products.findIndex((p) => p.id === product.id);
    products[prodIndex] = updateProduct;
    clearProd();
    editStatus = false;
  };

  const onSubmitHandler = () => {
    if (!editStatus) {
      addProduct();
    } else {
      updateProd();
      console.log("updated");
      editStatus = false;
    }
  };

  //content card Clean
  const clearProd = () => {
    product = {
      id: "",
      name: "",
      description: "",
      category: "",
      imageURL: "",
    };
  };

  //Delete Produc
  const deleteProd = (id) => {
    products = products.filter((product) => product.id !== id);
  };
  //Edit Produc
  const editProd = (prodEdited) => {
    product = prodEdited;
    editStatus = true;
  };
</script>

<main>
  <div class="container">
    <h1 class="text-center">Product Shop</h1>
    <div class="row">
      <div class="col-md-6">
        {#if !editStatus}
          <h2 class="text-center">New Product:</h2>
        {:else}
          <h2 class="text-center">Edit Product:</h2>
        {/if}
        <div class="card">
          <form on:submit|preventDefault={onSubmitHandler} action="">
            <div class="form-group">
              <input
                bind:value={product.name}
                class="form-control"
                type="text"
                name=""
                id="prod-name"
                placeholder="Product name"
              />
            </div>
            <div class="form-group">
              <textarea
                bind:value={product.description}
                class="form-control"
                id="prod-desc"
                rows="3"
                placeholder="Insert the product description "
              />
            </div>
            <div class="form-group">
              <select
                bind:value={product.category}
                class="form-control"
                id="category"
              >
                <option value="">--select one--</option>
                <option value="Laptop">Laptop</option>
                <option value="Desktop">Desktop</option>
                <option value="Server">Server</option>
                <option value="Other">Other</option>
              </select>
            </div>
            <div class="form-group">
              <input
                bind:value={product.imageURL}
                class="form-control"
                type="url"
                id="prod-img-url"
                placeholder="Insert URL Image"
              />
            </div>
            <button class="btn btn-lg btn-block btn-primary">
              {#if !editStatus}
                Save Product
              {:else}
                Update Product
              {/if}
            </button>
          </form>
        </div>
      </div>
      <div class="col-md-6">
        <h2 class="text-center">Products:</h2>
        {#if products.length > 0}
          {#each products as product}
            <div class="card mt-3">
              <div class="row">
                <div class="col-md-4">
                  {#if product.imageURL}
                    <img class="card-img" src={product.imageURL} alt="" />
                  {:else}
                    <img
                      class="card-img"
                      src="./images/imgNotFound.png"
                      alt=""
                    />
                  {/if}
                </div>
                <div class="col-md-5">
                  <h4>
                    <strong>{product.name}</strong>
                    <span><small>{product.category}</small></span>
                  </h4>
                  <p class="card-text">{product.description}</p>
                </div>
                <div class="col-md-3 mt-4">
                  <button
                    on:click={editProd(product)}
                    class="btn btn-sm btn-block btn-primary">Edit</button
                  >
                  <button
                    on:click={deleteProd(product.id)}
                    class="btn btn-danger btn-sm btn-block">Delete</button
                  >
                </div>
              </div>
            </div>
          {/each}
        {:else}
          <h3>No products to show</h3>
        {/if}
      </div>
    </div>
  </div>
</main>

<style>
</style>
