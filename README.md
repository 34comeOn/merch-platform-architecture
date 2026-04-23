# 📦 Яндекс Мерч: System Design Document
> **Live Demo:** https://yandex-merch.base44.app
> **Presentation:** https://storage.yandexcloud.net/mike/Yandex-Merch.pdf
> **System Design pdf:** https://storage.yandexcloud.net/mike/System%20design.pdf
> **User flow pdf:** https://storage.yandexcloud.net/mike/User%20flow.pdf

> **Executive Summary**: Трансформация хаотичного рынка корпоративного мерча в 
> прозрачную экосистему через AI-дизайн и модель умного распределения заказов.



## 🎯 1. Цели и задачи (Goals & Scope)
* **Vision**: Сократить путь от идеи до готового продукта с недель до минут.
* **Core Value**: Доверенная среда для B2B-сделок с гарантией качества от Яндекса.



## 🏗️ 2. Архитектурная стратегия (Architectural Strategy)
Мы используем подход **Microfrontends** и **Event-Driven Backend** для обеспечения максимальной отказоустойчивости.

## 🧩 Основные блоки:
1. **Catalog MFE** — легкая лента вдохновения.
2. **AI Design Lab** — тяжелый конструктор (Canvas/WebGL).
3. **Matching Engine** — диспетчер заказов (модель Яндекс такси).



## ⚙️ 3. Высокоуровневая схема (HLD)
### 🚀 Технологический стек:
* **Frontend**: React, Module Federation, Three.js/Fabric.js.
* **Backend**: Node.js (Sharp), Go (Matching Service), Kafka.
* **Infrastructure**: Yandex Cloud (S3, Managed Postgres, Redis).



## 🔄 4. Жизненный цикл данных (Data Flow)


| **Тип данных** | **Хранилище** | **Политика (Lifecycle)** |
| :--- | :---: | :--- |
| **Print-ready** | PDF	Yandex S3 (Cold) | Удаление через 30 дней после заказа |
| **UI Previews** | Yandex S3 (Hot) | Кэширование через CDN |
| **Order Metadata** | PostgreSQL | Бессрочное хранение (Транзакции) |



## 🚕 5. Диспетчеризация (Matching & Dispatch)
Система работает по принципу **обратного аукциона**:
* **Geo-sharding**: Поиск ближайшего производства для экономии на логистике **Яндекс Go**.
* **Escrow**: Безопасная сделка — деньги холдируются до подтверждения качества.
