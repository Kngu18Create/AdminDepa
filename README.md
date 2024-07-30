# AdminDepa
import React, { useState } from 'react';
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { 
  BarChart, 
  Bar, 
  XAxis, 
  YAxis, 
  CartesianGrid, 
  Tooltip, 
  Legend, 
  ResponsiveContainer,
  PieChart,
  Pie,
  Cell,
  LineChart,
  Line
} from 'recharts';
import { Home, Users, DollarSign, Wrench, AlertCircle } from 'lucide-react';

// Datos de ejemplo basados en las imágenes proporcionadas
const inquilinos = [
  { nombre: "David Samaniego", departamento: "101", estadoPago: "Pagado", montoAlquiler: 1850 },
  { nombre: "Diana Noguera", departamento: "102", estadoPago: "Pagado", montoAlquiler: 2050 },
  { nombre: "Janderson Feitoza", departamento: "201", estadoPago: "Pagado", montoAlquiler: 2350 },
  { nombre: "Gabriel Gonzalez", departamento: "202", estadoPago: "Atrasado", montoAlquiler: 2350 },
  { nombre: "Candida Santacruz", departamento: "203", estadoPago: "Atrasado", montoAlquiler: 1950 },
  { nombre: "Iglesia de Jesus", departamento: "204", estadoPago: "Pagado", montoAlquiler: 1750 },
  { nombre: "Gladys Garay", departamento: "301", estadoPago: "Atrasado", montoAlquiler: 2250 },
  { nombre: "Kelvyn Ferreira", departamento: "302", estadoPago: "Pagado", montoAlquiler: 2050 },
  { nombre: "Liliana Scappini", departamento: "303", estadoPago: "Pagado", montoAlquiler: 1850 },
  { nombre: "Jacqueline Garcia", departamento: "304", estadoPago: "Atrasado", montoAlquiler: 1850 },
  { nombre: "Blanca Valdez", departamento: "401", estadoPago: "Pagado", montoAlquiler: 1950 },
  { nombre: "Ivonne Battaglia", departamento: "402", estadoPago: "Pagado", montoAlquiler: 1950 },
  { nombre: "Steven Wiebe", departamento: "403", estadoPago: "Pagado", montoAlquiler: 1500 },
  { nombre: "Pablo Lugo", departamento: "404", estadoPago: "Atrasado", montoAlquiler: 1550 },
  { nombre: "Scarlet", departamento: "Salon Comercial", estadoPago: "Pagado", montoAlquiler: 3850 },
  { nombre: "Julio Cristaldo", departamento: "Duplex 1", estadoPago: "Atrasado", montoAlquiler: 3500 },
  { nombre: "Gerardo Martinez", departamento: "Duplex 2", estadoPago: "Atrasado", montoAlquiler: 3200 },
  { nombre: "Cesar Silva", departamento: "Lambare", estadoPago: "Atrasado", montoAlquiler: 3600 },
];

const balanceData = [
  { mes: "Junio", ingresosTotales: 16561273, egresosTotales: 26009121, saldoACobrar: 41400000 },
  { mes: "Julio", ingresosTotales: 9044656, egresosTotales: 57414465, saldoACobrar: 41400000 },
  { mes: "Agosto", ingresosTotales: 0, egresosTotales: 0, saldoACobrar: 41400000 },
  { mes: "Septiembre", ingresosTotales: 0, egresosTotales: 0, saldoACobrar: 41400000 },
];

const Dashboard = () => {
  const totalInquilinos = inquilinos.length;
  const inquilinosAlDia = inquilinos.filter(i => i.estadoPago === "Pagado").length;
  const inquilinosAtrasados = totalInquilinos - inquilinosAlDia;
  const montoTotalAlquiler = inquilinos.reduce((sum, i) => sum + i.montoAlquiler, 0);

  const estadoPagos = [
    { name: "Al día", value: inquilinosAlDia },
    { name: "Atrasados", value: inquilinosAtrasados },
  ];

  const COLORS = ['#00C49F', '#FF8042'];

  return (
    <div className="p-4">
      <h1 className="text-3xl font-bold mb-6">Dashboard de Gestión de Inmuebles</h1>
      
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Total Inquilinos</CardTitle>
            <Users className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">{totalInquilinos}</div>
          </CardContent>
        </Card>
        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Monto Total de Alquiler</CardTitle>
            <DollarSign className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">₲ {montoTotalAlquiler.toLocaleString()}</div>
          </CardContent>
        </Card>
        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Inquilinos al Día</CardTitle>
            <AlertCircle className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">{inquilinosAlDia}</div>
          </CardContent>
        </Card>
        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Inquilinos Atrasados</CardTitle>
            <AlertCircle className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">{inquilinosAtrasados}</div>
          </CardContent>
        </Card>
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-8">
        <Card>
          <CardHeader>
            <CardTitle>Estado de Pagos</CardTitle>
          </CardHeader>
          <CardContent>
            <ResponsiveContainer width="100%" height={300}>
              <PieChart>
                <Pie
                  data={estadoPagos}
                  cx="50%"
                  cy="50%"
                  labelLine={false}
                  outerRadius={80}
                  fill="#8884d8"
                  dataKey="value"
                >
                  {estadoPagos.map((entry, index) => (
                    <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                  ))}
                </Pie>
                <Tooltip />
                <Legend />
              </PieChart>
            </ResponsiveContainer>
          </CardContent>
        </Card>

        <Card>
          <CardHeader>
            <CardTitle>Balance Mensual</CardTitle>
          </CardHeader>
          <CardContent>
            <ResponsiveContainer width="100%" height={300}>
              <LineChart data={balanceData}>
                <CartesianGrid strokeDasharray="3 3" />
                <XAxis dataKey="mes" />
                <YAxis />
                <Tooltip />
                <Legend />
                <Line type="monotone" dataKey="ingresosTotales" stroke="#8884d8" name="Ingresos" />
                <Line type="monotone" dataKey="egresosTotales" stroke="#82ca9d" name="Egresos" />
                <Line type="monotone" dataKey="saldoACobrar" stroke="#ffc658" name="Saldo a Cobrar" />
              </LineChart>
            </ResponsiveContainer>
          </CardContent>
        </Card>
      </div>

      <Card>
        <CardHeader>
          <CardTitle>Detalle de Inquilinos</CardTitle>
        </CardHeader>
        <CardContent>
          <div className="overflow-x-auto">
            <table className="min-w-full bg-white">
              <thead className="bg-gray-100">
                <tr>
                  <th className="py-2 px-4 border-b">Nombre</th>
                  <th className="py-2 px-4 border-b">Departamento</th>
                  <th className="py-2 px-4 border-b">Estado de Pago</th>
                  <th className="py-2 px-4 border-b">Monto de Alquiler</th>
                </tr>
              </thead>
              <tbody>
                {inquilinos.map((inquilino, index) => (
                  <tr key={index} className={index % 2 === 0 ? 'bg-gray-50' : 'bg-white'}>
                    <td className="py-2 px-4 border-b">{inquilino.nombre}</td>
                    <td className="py-2 px-4 border-b">{inquilino.departamento}</td>
                    <td className={`py-2 px-4 border-b ${inquilino.estadoPago === 'Pagado' ? 'text-green-600' : 'text-red-600'}`}>
                      {inquilino.estadoPago}
                    </td>
                    <td className="py-2 px-4 border-b">₲ {inquilino.montoAlquiler.toLocaleString()}</td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </CardContent>
      </Card>
    </div>
  );
};

export default Dashboard;
