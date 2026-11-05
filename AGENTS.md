<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.
<!-- LOVABLE:END -->

## Architecture
- Each practice (layers/broilers/kienyeji) is a `farms` row; all record tables carry `farm_id` + `user_id` with owner-only RLS, so one account can run several practices.
- Which dashboard sections a practice shows is defined only in `src/lib/practices.ts` (single source of truth for practice differences).
- Dashboard data is read/written from the browser client via `src/lib/farm-data.ts` hooks (RLS enforces ownership); no server functions needed.
- Shared farm tables own record search and local CSV export; form values reset only on mutation success to preserve input on failed saves.
- The root-mounted theme switcher applies semantic dark tokens after hydration and persists appearance locally; treatment catalog labels are centralized and store in the existing treatment name field without dosing advice.
