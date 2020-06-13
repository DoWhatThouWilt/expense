<script>
  import {
    Collapse,
    Navbar,
    NavbarToggler,
    NavbarBrand,
    Nav,
    NavItem,
    NavLink,
    UncontrolledDropdown,
    DropdownToggle,
    DropdownMenu,
    DropdownItem
  } from 'sveltestrap';

  import { url, isActive } from "@sveltech/routify";

  const _links = [
      ["/index", "Home"],
      ["./testing", "Testing"],
      ["./calc", "Calc"]
  ]

  let isOpen = false;

  function handleUpdate(event) {
    isOpen = event.detail.isOpen;
  }
</script>

<Navbar class="indigo lighten-1 z-depth-2" dark expand="md">
  <div class="container">
      <NavbarBrand href={$url("/index")}><img class="logo" src="images/knot2.png" height="50" alt="mdb logo"><span class="brand">Calculatron</span></NavbarBrand>
      <NavbarToggler color="" on:click={() => (isOpen = !isOpen)} />
      <Collapse {isOpen} navbar expand="md" on:update={handleUpdate}>
        <Nav class="ml-auto" navbar>
        {#each _links as [path, name]}
              <li class="nav-item" class:active={$isActive(path)}>
                <NavLink href={$url(path)}>{name}</NavLink>
              </li>
          {/each}
          <UncontrolledDropdown nav inNavbar>
            <DropdownToggle nav caret>Options</DropdownToggle>
            <DropdownMenu right>
              <DropdownItem>Option 1</DropdownItem>
              <DropdownItem>Option 2</DropdownItem>
              <DropdownItem divider />
              <DropdownItem>Reset</DropdownItem>
            </DropdownMenu>
          </UncontrolledDropdown>
        </Nav>
      </Collapse>
  </div>
</Navbar>

<style>
    .brand {
        font-weight: 375;
        margin-left: 10px;
    }

    .logo {
      filter: invert();
      -webkit-filter: invert(100%);
    }
</style>
