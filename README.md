# CABY26 Dataset

Cyber-Aggression Bystander Roles 2026 (CABY26) is a relabeled cyberbullying dataset built from Twitter conversation threads (main post + replies). Each thread and each reply was independently re-annotated by a panel of annotators, with majority-vote labels, per-item agreement scores, and a tie-break resolution path recorded. The original CyBy24 dataset's labels are also carried over on each file for comparison against the new CABY26 labels.

The dataset consists of two files:

- `caby26_threads.csv` — one row per thread (the main post)
- `caby26_replies.csv` — one row per reply, linked to its thread via `thread_id`

## `caby26_threads.csv`

2,781 rows. One row per thread.

| Column | Description |
|---|---|
| `thread_id` | Unique identifier for the thread. Joins to `caby26_replies.csv.thread_id`. |
| `main_post_text` | Text of the thread's main post. |
| `main_post_label` | CABY26 majority-vote label for the main post: `Aggression` or `No Aggression`. |
| `cy24_cyberbullying_label` | Original CyBy24 label for this **main post specifically**, matched from the CY24 standalone-tweet file by exact text match (not the thread-level label — see note below). One of: `Normal`, `Aggression (No Bullying)`, `Bullying with low aggression`, `Bullying with high aggression`. Blank for 3 threads whose main post text does not exist anywhere in the CY24 file. |
| `thread_label` | CABY26 majority-vote label for the thread as a whole (main post + replies): `Aggression` or `No Aggression`. |
| `cyby24_cyberbullying_label` | Original CyBy24 **thread-level** label, carried over for comparison. One of: `Normal`, `Aggression (not bullying)`, `Bullying with low aggression`, `Bullying with high aggression`. |

Label distribution — `main_post_label`: Aggression 1,792 · No Aggression 989.
Label distribution — `thread_label`: Aggression 1,926 · No Aggression 855.
Label distribution — `cyby24_cyberbullying_label`: Aggression (not bullying) 1,401 · Normal 787 · Bullying with low aggression 473 · Bullying with high aggression 120.
Label distribution — `cy24_cyberbullying_label`: Normal 1,997 · Aggression (No Bullying) 670 · Bullying with low aggression 86 · Bullying with high aggression 25 · blank (no match in CY24) 3.

**Note on the two CY24 columns:** `cyby24_cyberbullying_label` and `cy24_cyberbullying_label` are *not* duplicates. `cyby24_cyberbullying_label` is CY24's original **thread-level** label (aggregated across the main post and all its replies). `cy24_cyberbullying_label` is the label for the **main post tweet only**, obtained by matching `main_post_text` against CY24's standalone-tweet file. 

## `caby26_replies.csv`

10,241 rows. One row per reply.

| Column | Description |
|---|---|
| `reply_id` | Identifier for the reply, unique within its thread (not globally unique — pair with `thread_id`). |
| `thread_id` | Identifier of the thread this reply belongs to. Joins to `caby26_threads.csv.thread_id`. |
| `reply_text` | Text of the reply. |
| `cyby24_bystander_role` | Original CyBy24 bystander role, carried over for comparison. One of: `instigator`, `defender`, `impartial`, `other`. |
| `bystander_role` | CABY26 majority-vote bystander role for this reply: `agree`, `disagree`, `impartial`, or `other`. |
| `vote_count` | Number of annotator votes agreeing with the majority label. |
| `total_votes` | Total number of annotator votes cast on this reply. |
| `agreement_score` | Inter-annotator agreement score (`vote_count / total_votes`). |
| `resolution_method` | How the final label was reached: `panel_majority` (a clear majority among the annotator panel) or `human_tiebreak` (a human adjudicator broke a tie). |

Label distribution — `bystander_role`: agree 4,990 · disagree 2,374 · impartial 2,037 · other 840.
Label distribution — `cyby24_bystander_role`: instigator 3,134 · defender 3,017 · impartial 2,145 · other 1,945.

## Joining the two files

`caby26_replies.csv` links to `caby26_threads.csv` via `thread_id`. A given `reply_id` is only unique within its thread, so join on the pair `(thread_id, reply_id)` if you need to address a specific reply.

## Provenance

CABY26 is a relabeling of the CyBy24 dataset's threads and replies. The `cyby24_cyberbullying_label` and `cyby24_bystander_role` columns preserve CyBy24's original labels alongside the new CABY26 annotations, allowing direct comparison between the two labeling schemes.

## License

This dataset is released under the **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)** license. You are free to share and adapt the dataset for non-commercial purposes, with attribution, under the same license terms. See https://creativecommons.org/licenses/by-nc/4.0/ for the full license text.

## Contact / Attribution

**SLL Research Group** (Syaheerah Lebai Lutfi Research Group)
Email: syaheerah@usm.my
