<script>
  import { getContext } from "svelte";
  export let id, name, amount

  import "@smui/list/bare.css";
  import List, {
    Item,
    Text,
    PrimaryText,
    SecondaryText,
    Graphic,
    Meta,
    Label,
    Group,
    Subheader,
    Separator
  } from "@smui/list/bare.js";

  const removeExpense = getContext("remove");
  const setModifiedExpense = getContext("modify");
</script>

<Item>
  <Graphic on:click={setModifiedExpense(id)}>
    <i class="fas fa-lg fa-pen quaternary-txt" />
  </Graphic>
  <Text>
    <PrimaryText class="primary-txt">{name}</PrimaryText>
    <SecondaryText class="secondary-txt">
      ${amount}
    </SecondaryText>
  </Text>
  <Meta on:click={removeExpense(id)}>
    <i class="fas fa-lg fa-trash tertiary-txt mr-1" />
    <!-- <a class="btn-floating secondary-bg ripple"><i class="fas fa-lg fa-trash-alt"></i></a> -->
  </Meta>
</Item>
<Separator />
