<template>
    <head>
        <link rel="stylesheet" href="https://unpkg.com/bootstrap@5.3.3/dist/css/bootstrap.min.css">
        <link rel="stylesheet" href="https://unpkg.com/bs-brain@2.0.4/components/heroes/hero-1/assets/css/hero-1.css">
    </head>

  
        <section class="bsb-hero-1 px-3 bsb-overlay " style="background-image: url(/src/assets/images/hero-back.jpg);">
            <div class="container">
                <div class="row justify-content-md-center">
                    <div class="col-12 col-md-11 col-lg-9 col-xl-7 col-xxl-6 text-center text-white">
                        <h2 class="display-3 fw-bold mb-3">Vue Starter</h2>
                        <p class="lead mb-5">This is my first vue project</p>
                        <div class="d-grid gap-2 d-sm-flex justify-content-sm-center">
                        <button type="button" class="btn bsb-btn-xl btn-light gap-3">About Me</button>
                        <button type="button" class="btn bsb-btn-xl btn-outline-light"> <RouterLink to="/to-do">To-Do</RouterLink> </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>
     
  </template>
  
  <style scoped>

   </style>
  