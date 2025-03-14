<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestión de Productos</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
</head>
<body>
    <div class="container mt-4">
        <h2 class="text-center">Gestión de Productos</h2>
        <div class="row">
            <div class="col-md-6 offset-md-3">
                <form id="productForm">
                    <div class="mb-3">
                        <label class="form-label">Producto ID</label>
                        <input type="text" id="productoId" class="form-control" required>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Nombre</label>
                        <input type="text" id="productoNombre" class="form-control" required>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Precio</label>
                        <input type="number" id="productoPrecio" class="form-control" required>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Cantidad</label>
                        <input type="number" id="productoCantidad" class="form-control" required>
                    </div>
                    <button type="button" class="btn btn-primary w-100" onclick="agregarProducto()">
                        <i class="fas fa-plus"></i> Agregar Producto
                    </button>
                </form>
            </div>
        </div>

        <table class="table table-bordered mt-4">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nombre</th>
                    <th>Precio</th>
                    <th>Cantidad</th>
                    <th>SubTotal</th>
                </tr>
            </thead>
            <tbody id="productosTabla">
            </tbody>
        </table>

        <div class="mt-4">
            <label>SubTotal:</label>
            <input type="text" id="subtotal" class="form-control" readonly>
            <label>Descuento (10%):</label>
            <input type="text" id="descuento" class="form-control" readonly>
            <label>ISV (15%):</label>
            <input type="text" id="isv" class="form-control" readonly>
            <label>Total a Pagar:</label>
            <input type="text" id="total" class="form-control" readonly>
        </div>
    </div>

    <script>
        function agregarProducto() {
            let id = document.getElementById("productoId").value;
            let nombre = document.getElementById("productoNombre").value;
            let precio = parseFloat(document.getElementById("productoPrecio").value);
            let cantidad = parseInt(document.getElementById("productoCantidad").value);
            let subtotal = precio * cantidad;
            
            let tabla = document.getElementById("productosTabla");
            let fila = tabla.insertRow();
            fila.innerHTML = `<td>${id}</td><td>${nombre}</td><td>${precio.toFixed(2)}</td><td>${cantidad}</td><td>${subtotal.toFixed(2)}</td>`;
            
            actualizarTotales();
            document.getElementById("productForm").reset();
        }

        function actualizarTotales() {
            let filas = document.querySelectorAll("#productosTabla tr");
            let subtotal = 0;
            filas.forEach(fila => {
                let sub = parseFloat(fila.cells[4].innerText);
                subtotal += sub;
            });
            let descuento = subtotal * 0.10;
            let isv = subtotal * 0.15;
            let total = subtotal - descuento + isv;
            
            document.getElementById("subtotal").value = subtotal.toFixed(2);
            document.getElementById("descuento").value = descuento.toFixed(2);
            document.getElementById("isv").value = isv.toFixed(2);
            document.getElementById("total").value = total.toFixed(2);
        }
    </script>
</body>
</html>
