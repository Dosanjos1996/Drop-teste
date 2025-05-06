import Link from "next/link";
import { ShoppingCart } from 'lucide-react';
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Badge } from "@/components/ui/badge";
import { produtos } from "@/lib/produtos";

export default function Home() {
  const produtosDestaque = produtos.slice(0, 4);

  return (
    <div className="container mx-auto px-4 py-8">
      {/* Hero Section */}
      <section className="bg-gradient-to-r from-blue-600 to-blue-800 rounded-lg p-8 mb-12 text-white">
        <div className="max-w-3xl">
          <h1 className="text-4xl font-bold mb-4">Bem-vindo à nossa Loja de Produtos Populares</h1>
          <p className="text-xl mb-6">Encontre os melhores produtos com os melhores preços!</p>
          <Button asChild size="lg" className="bg-white text-blue-700 hover:bg-gray-100">
            <Link href="/produtos">Ver Produtos</Link>
          </Button>
        </div>
      </section>

      {/* Featured Products */}
      <section className="mb-12">
        <div className="flex justify-between items-center mb-6">
          <h2 className="text-2xl font-bold">Produtos em Destaque</h2>
          <Link href="/produtos" className="text-blue-600 hover:underline">
            Ver todos
          </Link>
        </div>
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
          {produtosDestaque.map((produto) => (
            <Card key={produto.id} className="overflow-hidden group">
              <div className="relative h-48 bg-gray-100">
                <img
                  src={produto.imagem || "/placeholder.svg"}
                  alt={produto.nome}
                  className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300"
                />
                {produto.promocao && (
                  <Badge className="absolute top-2 right-2 bg-red-500">Promoção</Badge>
                )}
              </div>
              <CardContent className="p-4">
                <h3 className="font-semibold mb-2">{produto.nome}</h3>
                <div className="flex justify-between items-center">
                  <div>
                    {produto.promocao ? (
                      <div>
                        <span className="text-gray-500 line-through text-sm">
                          R$ {produto.precoOriginal.toFixed(2)}
                        </span>
                        <span className="text-red-600 font-bold ml-2">
                          R$ {produto.preco.toFixed(2)}
                        </span>
                      </div>
                    ) : (
                      <span className="font-bold">R$ {produto.preco.toFixed(2)}</span>
                    )}
                  </div>
                  <Button asChild variant="outline" size="sm">
                    <Link href={`/produtos/${produto.id}
