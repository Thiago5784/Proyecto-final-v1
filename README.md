# Proyecto-final-v1
package sistemaventas;
import sistemaventas.dao.*;
import sistemaventas.entity.*;

import java.util.Date;

public class Main {
    public static void main(String[] args) {
        // DAO
        ClienteDAO clienteDAO = new ClienteDAO();
        ProductoDAO productoDAO = new ProductoDAO();
        VentaDAO ventaDAO = new VentaDAO();
        DetalleVentaDAO detalleDAO = new DetalleVentaDAO();

        // Crear y registrar clientes
        Cliente cliente1 = new Cliente(1, "Juan Pérez", "juan@example.com");
        Cliente cliente2 = new Cliente(2, "Ana Gómez", "ana@example.com");
        clienteDAO.insertar(cliente1);
        clienteDAO.insertar(cliente2);

        // Crear y registrar productos
        Producto producto1 = new Producto(1, "Laptop", 2500.00);
        Producto producto2 = new Producto(2, "Mouse", 100.00);
        productoDAO.insertar(producto1);
        productoDAO.insertar(producto2);

        // Crear y registrar una venta
        Venta venta1 = new Venta(1, cliente1.getId(), new Date());
        ventaDAO.insertar(venta1);

        // Crear y registrar detalles de venta
        DetalleVenta detalle1 = new DetalleVenta(1, venta1.getId(), producto1.getId(), 1);
        DetalleVenta detalle2 = new DetalleVenta(2, venta1.getId(), producto2.getId(), 2);
        detalleDAO.insertar(detalle1);
        detalleDAO.insertar(detalle2);

        // Mostrar clientes
        System.out.println("=== Clientes ===");
        for (Cliente c : clienteDAO.obtenerTodos()) {
            System.out.println(c.getId() + ": " + c.getNombre() + " - " + c.getCorreo());
        }

        // Mostrar productos
        System.out.println("\n=== Productos ===");
        for (Producto p : productoDAO.obtenerTodos()) {
            System.out.println(p.getId() + ": " + p.getNombre() + " - S/. " + p.getPrecio());
        }

        // Mostrar ventas
        System.out.println("\n=== Ventas ===");
        for (Venta v : ventaDAO.obtenerTodos()) {
            System.out.println("Venta ID: " + v.getId() + " - Cliente ID: " + v.getClienteId() + " - Fecha: " + v.getFecha());
        }

        // Mostrar detalles de venta
        System.out.println("\n=== Detalles de Venta ===");
        for (DetalleVenta d : detalleDAO.obtenerTodos()) {
            System.out.println("Detalle ID: " + d.getId() + " - Venta ID: " + d.getVentaId() +
                               " - Producto ID: " + d.getProductoId() + " - Cantidad: " + d.getCantidad());
        }
    }
}
