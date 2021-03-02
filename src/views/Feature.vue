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
            <div class="col-md-1">
                <label for="code" class="form-label">Code</label>
                <input type="text" class="form-control" id="code" />
            </div>
            <div class="col-md-7">
                <label for="parent" class="form-label">Parent</label>
                <select class="form-select" id="parent">
                    <option selected disabled value></option>
                    <option value="2">Config > Users</option>
                </select>
            </div>
            
            <button type="submit" class="btn btn-primary">Search</button>
        </form>
    </div>
</template>