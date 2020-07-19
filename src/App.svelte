<script>
  let nombre = "jhonnatan";
  let enable = false;

  function saludar() {
    alert("hola");
  }

  const nombres = ["jhonnatan", "andres", "urueña", "diaz"];
  const _url = "https://jsonplaceholder.typicode.com/users";

  let promesa = Get_info();
  let users = [];

  function sleep(s) {
    return new Promise(res => setTimeout(res, s));
  }

  async function Get_info() {
    const res = await fetch(_url);

    users = await res.json();
    await sleep(4000);
    if (res.ok) return users;
    else throw new Error("Error");
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
<h1>binding</h1>
  <h2>{nombre}</h2>
  <input type="text" bind:value={nombre} />
  <input type="checkbox" bind:checked={enable} />
  <input type="button" value="Enviar" disabled={!enable} />
  <button on:click={saludar}>Saludar</button>
<hr/>

<h1>For each</h1>
  <ul>
    {#each nombres as nombre, i}
      <li>{i + 1} {nombre}</li>
    {/each}
  </ul>
<hr/>

<h1>Promesas</h1>
  <table align="center">
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Apellido</th>
        <th>email</th>
      </tr>
    </thead>
    <tbody>

      {#await promesa}
        <p>Cargando el API</p>
      {:then usuarios}
        {#each users as persona}
          <tr>
            <td>{persona.name}</td>
            <td>{persona.username}</td>
            <td>{persona.email}</td>
          </tr>
        {/each}

      {/await}

    </tbody>
  </table>
</main>
