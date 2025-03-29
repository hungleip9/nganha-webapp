<template>
  <div class="border">
    <!--begin::Input group-->
    <div class="input-group mb-5">
      <span class="input-group-text" id="basic-addon1">@</span>
      <input
        type="text"
        class="form-control"
        placeholder="Username"
        aria-label="Username"
        aria-describedby="basic-addon1"
      />
    </div>
    <!--end::Input group-->

    <!--begin::Input group-->
    <div class="input-group mb-5">
      <input
        type="text"
        class="form-control"
        placeholder="Recipient's username"
        aria-label="Recipient's username"
        aria-describedby="basic-addon2"
      />
      <span class="input-group-text" id="basic-addon2">@example.com</span>
    </div>
    <!--end::Input group-->

    <!--begin::Input group-->
    <label for="basic-url" class="form-label">Your vanity URL</label>
    <div class="input-group mb-5">
      <span class="input-group-text" id="basic-addon3"
        >https://example.com/users/</span
      >
      <input
        type="text"
        class="form-control"
        id="basic-url"
        aria-describedby="basic-addon3"
      />
    </div>
    <!--end::Input group-->

    <!--begin::Input group-->
    <div class="input-group mb-5">
      <span class="input-group-text">$</span>
      <input
        type="text"
        class="form-control"
        aria-label="Amount (to the nearest dollar)"
      />
      <span class="input-group-text">.00</span>
    </div>
    <!--end::Input group-->

    <!--begin::Input group-->
    <div class="input-group mb-5">
      <input
        type="text"
        class="form-control"
        placeholder="Username"
        aria-label="Username"
      />
      <span class="input-group-text">@</span>
      <input
        type="text"
        class="form-control"
        placeholder="Server"
        aria-label="Server"
      />
    </div>
    <!--end::Input group-->

    <!--begin::Input group-->
    <div class="input-group">
      <span class="input-group-text">With textarea</span>
      <textarea class="form-control" aria-label="With textarea"></textarea>
    </div>
    <!--end::Input group-->
    <hr/>
    <div class="table-responsive">
      <table class="table table-striped gy-7 gs-7">
        <thead>
          <tr
            class="fw-semibold fs-6 text-gray-800 border-bottom-2 border-gray-200"
          >
            <th class="min-w-200px">Name</th>
            <th class="min-w-400px">Position</th>
            <th class="min-w-100px">Office</th>
            <th class="min-w-200px">Age</th>
            <th class="min-w-200px">Start date</th>
            <th class="min-w-200px">Salary</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="i in 20">
            <td>Tiger Nixon</td>
            <td>System Architect</td>
            <td>Edinburgh</td>
            <td>61</td>
            <td>2011/04/25</td>
            <td>$320,800</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped></style>
