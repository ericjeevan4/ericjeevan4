# How the Contribution Snake Works

This explains what the snake animation on the profile README is actually showing.

## The boxes are real, not decorative

Every box in the snake's grid is pulled directly from your real GitHub contribution
graph — the same calendar shown on your profile page ("X contributions in the last
year"). The workflow does not generate, sample, or fake any data.

- **Green boxes** = your real contribution days (darker/brighter green = more
  contributions that day, same scale as your profile calendar)
- **Grey / empty boxes** = days with no contributions — these were never green,
  the snake isn't skipping or hiding anything
- If an account has zero contributions, the snake has nothing to eat and the
  board is just all-grey

The snake itself is purely a visual animation layered on top of this real data —
it moves across the grid and "eats" the green squares in sequence, turning them
empty as it passes.

## It updates once a day, not live

The `Generate Profile Assets` workflow (`.github/workflows/snake.yml`) runs on a
daily cron schedule. That means:

- The snake reflects your contributions **as of the last scheduled run**, not
  in real time
- A commit pushed today won't show as a green square on the snake until the
  next scheduled run
- To sync it immediately after making changes, go to the **Actions** tab on
  the repo → select **Generate Profile Assets** → **Run workflow** to trigger
  it manually

## Where the data comes from

The `Platane/snk` action queries GitHub's own contribution API for the
configured username and renders the grid + snake as a static SVG, which is
committed to the `output` branch and referenced by the README. No third-party
service is involved — same as the self-hosted trophy SVG.
