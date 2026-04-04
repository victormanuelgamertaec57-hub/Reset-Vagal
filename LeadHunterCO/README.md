# 🎯 LEAD HUNTER CO v1.0

**Google Maps Lead Generation Tool para Colombia**  
Por: BlackCats Agency / Skuall Studio | Créditos: Cristian Saenz

---

## ¿Qué hace?

Escanea automáticamente Google Maps en **12 ciudades colombianas** × **14 nichos de negocio** para identificar negocios que necesitan servicios web. Para cada lead:

1. **Busca** negocios por categoría y ciudad via Google Places API
2. **Extrae** datos completos: nombre, dirección, teléfono, reseñas, rating, horario, web
3. **Valida** si tienen sitio web y su calidad (HTTPS, velocidad, mobile)
4. **Analiza** reseñas para detectar señales de dolor y mercado internacional
5. **Califica** cada lead con un score 0-100 basado en 8 criterios ponderados
6. **Genera** un argumento de venta personalizado de 10 segundos
7. **Exporta** a Excel estilizado + JSON con Pipeline CRM incluido

---

## Requisitos

- Python 3.8+
- Google Places API Key ([obtener aquí](https://console.cloud.google.com/apis/library/places-backend.googleapis.com))
- Librerías: `requests`, `openpyxl`

## Instalación

```bash
pip install requests openpyxl
```

## Uso Rápido (CLI)

```bash
# Con API Key como variable de entorno
export GOOGLE_PLACES_API_KEY="tu-api-key-aqui"
python lead_hunter_co.py

# O ingresarla manualmente al ejecutar
python lead_hunter_co.py
```

## Uso como Módulo (Python)

```python
from lead_hunter_co import LeadHunterEngine, CIUDADES, NICHOS

# Inicializar
engine = LeadHunterEngine(api_key="tu-api-key")

# Escaneo completo (todas las ciudades y nichos)
leads = engine.scan()

# Escaneo parcial
leads = engine.scan(
    ciudades={"Bogotá": CIUDADES["Bogotá"], "Medellín": CIUDADES["Medellín"]},
    nichos={"Gastronomía": NICHOS["Gastronomía"]},
    max_per_query=5,
    validate_webs=True
)

# Exportar
engine.export_excel("mis_leads.xlsx")
engine.export_json("mis_leads.json")
```

---

## Scoring (0-100)

| Criterio               | Peso | Descripción |
|------------------------|------|-------------|
| Sin sitio web          | 25%  | No tiene web = máx puntos |
| Volumen de reseñas     | 25%  | +500 = máx; 100-500 = medio |
| Nicho alto impacto     | 15%  | Salud, gastronomía, hotelería |
| Rating alto (≥4.3)     | 10%  | Merece presencia digital |
| Dolor en reseñas       | 10%  | Quejas solucionables con tech |
| Mercado internacional  | 5%   | Reseñas en inglés |
| Ticket potencial       | 5%   | Complejidad del proyecto |
| Urgencia temporal      | 5%   | Cambio dirección, temporada |

**Prioridad:** 🔴 ALTA (80-100) | 🟡 MEDIA (60-79) | 🟢 BAJA (40-59)

---

## Ciudades Cubiertas

Bogotá, Medellín, Cali, Barranquilla, Cartagena, Bucaramanga, Santa Marta, Pereira, Manizales, Ibagué, Villavicencio, Cúcuta

## Nichos Cubiertas

Plomería, HVAC, Electricista, Medicina Estética, Spa/Bienestar, Odontología, Veterinaria, Gastronomía, Fitness, Barbería, Fisioterapia, Taller Automotriz, Lavado Autos, Hotelería

---

## Costo API Estimado

Google Places API cobra ~$0.017 por text_search y ~$0.017 por place_details.  
Escaneo completo (~500 queries): **~$17 USD**  
Escaneo parcial (2 ciudades × 3 nichos): **~$3 USD**

---

## Output

Los archivos se guardan en `~/Documents/LeadHunterCO/`:
- `leads_colombia_YYYYMMDD_HHMM.xlsx` — Excel con Dashboard + Leads + CRM
- `leads_colombia_YYYYMMDD_HHMM.json` — JSON para integración con CRM/n8n

## Licencia

Uso exclusivo BlackCats Agency / Skuall Studio.
