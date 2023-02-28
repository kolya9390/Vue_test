<template>
  <footer class="py-3 bg-light">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-12 col-md-6 text-center text-md-left mb-3 mb-md-0">
          <p class="m-0 text-muted">&copy; {{ new Date().getFullYear() }} - Your Company Name</p>
        </div>
        <div class="col-12 col-md-6 text-center text-md-right">
          <ul class="list-inline mb-0">
            <li class="list-inline-item">
              <a href="#" class="text-muted">About</a>
            </li>
            <li class="list-inline-item">
              <a href="#" class="text-muted">Help</a>
            </li>
            <li class="list-inline-item">
              <a href="#" class="text-muted">Contact</a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </footer>
</template>
<style>
.bg-light {
  background-color: #f8f9fa !important;
}

.footer-link {
  color: #6c757d;
  text-decoration: none;
  transition: color 0.3s ease-in-out;
}

.footer-link:hover {
  color: #343a40;
}
</style>



