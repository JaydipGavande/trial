<!doctype html>
<html lang="mr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Data Entry Website</title>

    <!-- Bootstrap -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />

    <style>
      body {
        min-height: 100vh;
        background-image: url("https://cdn.pixabay.com/photo/2019/08/26/12/32/feather-4431599_1280.jpg");
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
      }

      .card {
        border-radius: 15px;
        background-image: url("https://images.unsplash.com/photo-1625225230517-7426c1be750c?fm=jpg&q=60&w=3000");
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
      }

      label {
        color: black;
        font-weight: 500;
      }

      h3 {
        color: black;
      }

      * {
        box-sizing: border-box;
      }

      body {
        overflow-x: hidden;
      }

      .card {
        width: 100%;
        max-width: 100%;
      }

      table {
        width: 100%;
        max-width: 100%;
        table-layout: fixed;
      }

      th,
      td {
        word-break: break-word;
        white-space: normal;
        overflow-wrap: break-word;
      }
    </style>
  </head>

  <body>
    <div
      class="container min-vh-100 d-flex justify-content-center align-items-center px-3"
    >
      <div class="row w-100 justify-content-center">
        <div class="col-12 col-sm-10 col-md-8 col-lg-6 col-xl-5">
          <div class="card p-4 shadow-lg">
            <h3 class="text-center mb-4">Field Data</h3>

            <form id="dataForm">
              <div class="mb-3">
                <label class="form-label">NAME</label>
                <input type="text" class="form-control" name="name" required />
              </div>

              <div class="mb-3">
                <label class="form-label">MO NUMBER</label>
                <input type="tel" class="form-control" name="mobile" required />
              </div>

              <div class="mb-3">
                <label class="form-label">GMAIL</label>
                <input type="email" class="form-control" name="email" />
              </div>

              <button type="submit" class="btn btn-primary w-100 mt-3">
                Submit
              </button>
            </form>

            <hr class="text-white" />

            <div>
              <table class="table table-bordered table-light mt-3">
                <thead class="table-dark">
                  <tr>
                    <th>NAME</th>
                    <th>MOBILE</th>
                    <th>EMAIL</th>
                    <th>EDIT</th>
                  </tr>
                </thead>
                <tbody id="dataTable">
                  <!-- Dynamic data -->
                </tbody>
              </table>
            </div>

            <p id="msg" class="text-success text-center mt-3"></p>
          </div>
        </div>
      </div>
    </div>

    <script>
      const form = document.getElementById("dataForm");
const tableBody = document.getElementById("dataTable");

window.onload = function () {
    let savedData = JSON.parse(localStorage.getItem("fieldData")) || [];
    savedData.forEach((data, index) => addRow(data, index));
};

form.addEventListener("submit", function (e) {
    e.preventDefault();

    let name = form.name.value;
    let mobile = form.mobile.value;
    let email = form.email.value;

    let data = { name, mobile, email };

    let allData = JSON.parse(localStorage.getItem("fieldData")) || [];
    allData.push(data);
    localStorage.setItem("fieldData", JSON.stringify(allData));

    addRow(data, allData.length - 1);

    document.getElementById("msg").innerText = "Data Added Successfully ✔";
    form.reset();
});

function addRow(data, index) {
    let row = document.createElement("tr");

    row.innerHTML = `
        <td>${data.name}</td>
        <td>${data.mobile}</td>
        <td>${data.email}</td>
        <td>
            <button class="btn btn-danger btn-sm" onclick="deleteRow(${index})">
                Delete
            </button>
        </td>
    `;

    tableBody.appendChild(row);
}

function deleteRow(index) {
    let allData = JSON.parse(localStorage.getItem("fieldData")) || [];

    allData.splice(index, 1);
    localStorage.setItem("fieldData", JSON.stringify(allData));

    tableBody.innerHTML = "";
    allData.forEach((data, i) => addRow(data, i));
}
    
    </script>
  </body>
</html>
