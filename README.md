# GroupConnect V1

A private, internet-based group messaging website. Members authenticate with an account, and database Row Level Security prevents non-members from reading or sending group messages.

## What is included
- Responsive chat UI
- Email/password authentication
- Group/member data model
- Private group invitation concept
- Real-time message subscription
- PostgreSQL + RLS schema
- Secure separation between publishable frontend key and server secrets

## Setup
1. Create a Supabase project.
2. Open SQL Editor and run `supabase/schema.sql`.
3. In Supabase Realtime settings, disable public access for private channels.
4. Copy the Project URL and publishable key from the Supabase Connect/API settings.
5. Replace `YOUR_SUPABASE_URL` and `YOUR_SUPABASE_PUBLISHABLE_KEY` in `index.html`.
6. Host `index.html` on any static web host.

## Important next step for invitations
For production, invitations should be issued by a server-side Edge Function rather than allowing the browser to insert membership rows. The Edge Function should validate a short-lived invitation token, create the membership, and invalidate/revoke the token. Never put a Supabase secret/service-role key in the browser.

## Security model
The Group ID is an identifier, not authorization. Actual access is granted by membership rows and RLS. Supabase's publishable key can be used in the frontend when RLS is correctly configured; secret/service-role keys must remain server-side.
