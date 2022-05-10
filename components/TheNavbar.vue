<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark mb-3">
      <div class="container-fluid">
        <NuxtLink to="/" class="navbar-brand"> OnlineStore </NuxtLink>
        <button
          class="navbar-toggler"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
        >
          <span class="navbar-toggler-icon"> </span>
        </button>
        <div id="navbarSupportedContent" class="collapse navbar-collapse">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <NuxtLink to="/" class="nav-link" active-class="active">
                Home
              </NuxtLink>
            </li>
          </ul>
          <div class="d-flex">
            <button
              class="btn btn-primary"
              type="button"
              data-bs-toggle="offcanvas"
              data-bs-target="#offcanvasRight"
              aria-controls="offcanvasRight"
            >
              Shopping Cart
            </button>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>
