# Beca 18 RAG Chatbot

## Descripción
Chatbot de Recuperación Aumentada por Generación (RAG) que responde preguntas sobre el Reglamento Oficial de Beca 18 (PRONABEC, Perú). El sistema extrae fragmentos relevantes del PDF fuente y los usa como contexto para generar respuestas fundamentadas, sin depender del conocimiento paramétrico del modelo.

## Documento fuente
Resolución Directoral Ejecutiva N.° 033-2026-MINEDU/VMGI-PRONABEC

## Resumen del pipeline
El sistema extrae texto del PDF página por página, lo divide en chunks de 400 tokens con 60 de overlap, genera embeddings con gemini-embedding-001 y los almacena en ChromaDB con distancia coseno. Ante una pregunta, recupera los top-k fragmentos más relevantes y los pasa como contexto a gemini-2.5-flash para generar una respuesta citando páginas.

## Instalación
```bash
pip install -r requirements.txt
```

## Configuración de API Key
1. Obtén tu API key en https://aistudio.google.com/app/apikey
2. Copia `.env.example` a `.env`
3. Reemplaza `your_key_here` con tu key real
4. **Nunca subas `.env` a GitHub**

## Cómo correr el notebook
1. Abre `notebooks/beca18_rag_chatbot.ipynb` en Google Colab
2. Configura tu API key en Secrets de Colab como `GEMINI_API_KEY`
3. Sube `data/beca18_reglamento.pdf`
4. Ejecuta todas las celdas en orden

## Cómo usar el chat
- Escribe tu pregunta en el campo de texto
- Ajusta el slider `k` para controlar cuántos fragmentos recuperar
- Clic en **Ask** para obtener la respuesta
- Expande el accordion para ver las fuentes y páginas citadas
- Clic en **Clear** para limpiar el chat
