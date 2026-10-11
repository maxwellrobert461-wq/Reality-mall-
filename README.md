# REALITY MALL - Online Business Shopping

**Tagline:** Come to REALITY. Shop REALITY.

REALITY is Port Harcourt's first viral online business mall. Real shops, real products.

### What is REALITY?
Not Jumia. Not just shopping. REALITY is a mall where every product is a little sponsored ad.

- Sellers open shop themselves in 30 seconds
- They add products with WhatsApp link
- They choose VIRAL level:
    - **Starter ₦2,000** = Little Ad (bottom)
    - **Pro ₦5,000** = Viral (middle boost)
    - **Elite ₦10,000** = Super Viral TOP 🔥
- Buyers scroll homepage sorted by viral score. Click BUY = WhatsApp seller directly.
- No commission. No rent.

### How Money Flows
Sellers pay directly to owner:
**Moniepoint / Opay - 9078617514 - Odera Chidalu Vitalis**

### Tech Stack
- Frontend: HTML + Tailwind CSS
- Backend: Supabase (Postgres + RLS)
- Hosting: Vercel

### How Pages Work
- `index.html` = Public mall. Reads `products` table where status='approved', sorted by viral_score DESC.
- `dashboard.html` = Seller adds product → inserts into Supabase with status='pending' → shows Moniepoint/Opay payment → opens WhatsApp to Odera with proof.
- `admin.html` = Odera only. Shows all pending products. Click APPROVE → status='approved' → appears on homepage as viral.

### Setup
1. Create Supabase project
2. Run SQL in SQL Editor (see below)
3. Replace YOUR_SUPABASE_URL and YOUR_ANON_KEY in all html files
4. Deploy to Vercel

### Supabase SQL
create table products (
  id uuid default gen_random_uuid() primary key,
  name text, price int, image text, whatsapp text, shop_name text,
  plan text, viral_score int, payment_method text, payment_proof text,
  status text default 'pending', created_at timestamp default now()
);
alter table products enable row level security;
create policy "public read" on products for select using (true);
create policy "public insert" on products for insert with check (true);
create policy "public update" on products for update using (true);

Live: https://your-vercel-link.vercel.app
Owner: Odera Chidalu Vitalis - 9078617514