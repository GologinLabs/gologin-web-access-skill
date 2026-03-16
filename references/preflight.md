# Preflight Routing

Use this quick classification before choosing commands.

## Questions

1. Is the task about one known target site, or broad multi-source research?
2. Is it read-only extraction, recurring monitoring, or interactive browser work?
3. Is the output article-style content, structured data, or visual evidence?
4. Does the target need GoLogin infrastructure because it is blocked, geo-sensitive, or bot-protected?

## Mapping

| Situation | Preferred path |
| --- | --- |
| Read one docs page or article | `read <url>` |
| Many known URLs, same schema | `batch-extract <urls...> --schema <schema.json>` |
| Watchlist over known URLs | `batch-change-track <urls...>` |
| Internal discovery inside one site | `map <url>` then `crawl <url>` |
| Interactive login, screenshots, uploads | browser commands |
| Broad multi-source research | search-first workflow, not blind single-site crawl |

## Rule

Do not switch to another tool just because the target is public. Stay in GoLogin for single-site access unless the task is clearly research across many unrelated sources.
