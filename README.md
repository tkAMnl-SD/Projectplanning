# Projectplanning Machine supports

Eén statische pagina (`index.html`) met Supabase-login. Geen build nodig.

- **Hosting:** Vercel (Framework: *Other*, geen build command, output = root).
- **Database/login:** Supabase-project `rcevivqtbsqzwlwxwvep` (tabellen `projects`, `phases`, `comments`, `activity_log`, `settings`, `profiles`).
- **Rollen** (tabel `profiles`): `admin`, `editor` (alles bewerken), `viewer` (alleen eigen project inzien, kolom `project`).
- Alleen de *publishable key* staat in de code; toegang wordt afgedwongen door Row Level Security in de database.

## Gebruiker toevoegen
Supabase → Authentication → Users → *Invite user*. Daarna rol zetten:
```sql
update public.profiles set role='editor', initials='XX', full_name='Naam' where user_id=(select id from auth.users where email='naam@bedrijf.nl');
-- externe klant (alleen inzage in eigen project):
update public.profiles set role='viewer', project='Paprec' where user_id=(select id from auth.users where email='klant@bedrijf.com');
```
