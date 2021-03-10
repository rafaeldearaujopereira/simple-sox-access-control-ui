<template>
    <h2 class="text-start ms-3 p-3">Features</h2>
    <div class="container">
        <form class="row g-3">
            <div class="col-md-3">
                <label for="name" class="form-label">Name</label>
                <input type="text" class="form-control" id="name" />
            </div>
            <div class="col-md-4">
                <label for="description" class="form-label">Description</label>
                <input type="text" class="form-control" id="description" />
            </div>
            <div class="col-md-2">
                <label for="code" class="form-label">Code</label>
                <input type="text" class="form-control" id="code" />
            </div>
            <div class="col-md-7">
                <label for="parent" class="form-label">Parent</label>
                <select class="form-select" id="parent">
                    <option value=""></option>
                    <option value="2">Config > Users</option>
                </select>
            </div>
            <div class="col-md-2">
                <label for="parent" class="form-label">Type</label>
                <select class="form-select" id="parent">
                    <option value=""></option>
                    <option value="2">Menu</option>
                </select>
            </div>
            <div class="col-md-2 align-bottom">
            <button type="submit" class="btn btn-primary">Search</button>
            </div>
        </form>
        <br><br>        
        <table class="table table-sm table-bordered table-hover">
          <thead class="table-light">
          <tr>
            <th scope="col">Feature</th>
            <th scope="col">Type</th>
            <th scope="col">Parent</th>
            <th scope="col">Description</th>
          </tr>
          </thead>
          <tbody>
          <tr>
            <th scope="row">1</th>
            <td class="align-left">Mark</td>
            <td class="align-left">Otto</td>
            <td class="align-left">@mdo</td>
          </tr>
          <tr>
            <th scope="row">2</th>
            <td>Jacob</td>
            <td>Thornton</td>
            <td>@fat</td>
          </tr>
          <tr>
            <th scope="row">3</th>
            <td>Larry the Bird</td>
            <td>Larry the Bird</td>
            <td>@twitter</td>
          </tr>
          </tbody>
           <caption>Quantity of features: 3</caption>
        </table>

    </div>
</template>