<script>
import PasswordGenerator from "./lib/components/PasswordGenerator.svelte";

let name;
let email;
let password;
let password2;
let generatedPassword = "";

$: generatedPassword && console.log(generatedPassword);

</script>

<div class="container">
  <h1>Sign up</h1>
  <form autocomplete="off">
    <div class="form-group">
      <input type="text" id="name" class="form-control" placeholder="Name" bind:value={name} />
    </div>
    <div class="form-group">
      <input type="text" id="email" class="form-control" placeholder="Email" bind:value={email} />
    </div>
    <div class="form-group">
      <input type="password" id="password" class="form-control" placeholder="Password" bind:value={name} />
    </div>
    <div class="form-group">
      <input type="password" id="password2" class="form-control" placeholder="Confirm Password" bind:value={name} />
    </div>
    <PasswordGenerator generatedPassword={generatedPassword} />
    <div class="form-group">
      <button type="submit" class="btn btn-primary">Register</button>
    </div>
  </form>
</div>

<style>
  
</style>
