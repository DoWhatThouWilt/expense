<script>
    import Dialog, {
    Title,
    Content,
    Actions
  } from "@smui/dialog/bare.js";
  import "@smui/dialog/bare.css";
</script>

<style>
  .md-form label {
    font-size: 0.85em;
    margin-top: -0.7em;
  }
  .field {
    display: flex;
    flex-flow: column-reverse;
  }

  label,
  input {
    transition: all 0.2s;
    touch-action: manipulation;
  }

  input {
    margin-top: 1.25em;
    font-size: 1.25em;
    border: 0;
    border-bottom: 1px solid #ddd;
    font-family: inherit;
    -webkit-appearance: none;
    border-radius: 0;
    padding: 0;
    cursor: text;
  }

  input:focus {
    outline: 0;
    border-bottom: 1px solid #666;
  }
  input:placeholder-shown + label {
    cursor: text;
    max-width: 66.66%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    transform-origin: left bottom;
    transform: translate(0, 2.125rem) scale(1.5);
  }
  ::-webkit-input-placeholder {
    opacity: 0;
    transition: inherit;
  }
  input:focus::-webkit-input-placeholder {
    color: #ccc;
    opacity: 1;
  }
  input:not(:placeholder-shown) + label,
  input:focus + label {
    transform: translate(0, 0) scale(1);
    cursor: pointer;
  }
</style>

<div class="container">

  <div class="row justify-content-center">
    <div class="col-sm-12 col-md-8 col-lg-6 mt-5">
      <div class="card">

        <h5 class="card-header primary-bg white-text text-center py-4">
          <strong>Sign in</strong>
        </h5>

        <!--Card content-->
        <div class="card-body px-lg-5 pt-0">

          <!-- Form -->
          <form class="text-center" style="color: #757575;" action="#!">

            <div class="md-form field">
              <input placeholder="Name" type="text" class="form-control" />
              <label for="name">Name</label>
            </div>

            <div class="md-form field">
              <input placeholder="Amount" type="text" class="form-control" />
              <label for="amount">Amount</label>
            </div>

            <p class="quaternary-txt">Please fill out all the fields.</p>

            <button
              type="submit"
              class="btn btn-outline-info btn-block my-4 ripple">
              Submit
            </button>

          </form>
          <!-- Form -->

        </div>

      </div>
    </div>
  </div>
</div>
