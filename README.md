# @octokit/openapi-types

> [!NOTE]
> `@octokit/openapi-types` is currently outdated because Octokit lacks maintainers for the official Octokit JS repositories.
> This is my attempt at creating a working package.
>
> Issue: https://github.com/dsnsgithub/dsns.dev/issues/6


## Usage

Add to `package.json`:
```json
"overrides": {
    "@octokit/openapi-types": "github:dsnsgithub/openapi-types.ts#main"
},
```

### Optional 
Use this hack to typeguard:
```ts
import type { components } from "@octokit/openapi-types";

export type EventPayloadMap = {
  CreateEvent: components["schemas"]["create-event"];
  DeleteEvent: components["schemas"]["delete-event"];
  DiscussionEvent: components["schemas"]["discussion-event"];
  IssuesEvent: components["schemas"]["issues-event"];
  IssueCommentEvent: components["schemas"]["issue-comment-event"];
  ForkEvent: components["schemas"]["fork-event"];
  GollumEvent: components["schemas"]["gollum-event"];
  MemberEvent: components["schemas"]["member-event"];
  PublicEvent: components["schemas"]["public-event"];
  PushEvent: components["schemas"]["push-event"];
  PullRequestEvent: components["schemas"]["pull-request-event"];
  PullRequestReviewCommentEvent: components["schemas"]["pull-request-review-comment-event"];
  PullRequestReviewEvent: components["schemas"]["pull-request-review-event"];
  CommitCommentEvent: components["schemas"]["commit-comment-event"];
  ReleaseEvent: components["schemas"]["release-event"];
  WatchEvent: components["schemas"]["watch-event"];
};

function isEvent<T extends keyof EventPayloadMap>(
  event: components["schemas"]["event"],
  type: T
): event is components["schemas"]["event"] & { type: T; payload: EventPayloadMap[T] } {
  return event.type === type;
}
```

Example Usage:

```ts
import { Octokit } from "@octokit/rest";
import type { components } from "@octokit/openapi-types";

...

const res = await octokit.rest.activity.listPublicEventsForUser({
	username: "dsnsgithub",
	per_page: 30,
	headers: { "X-GitHub-Api-Version": "2022-11-28" }
})

for (const event of res.data) {
	if (isEvent(event, "PullRequestEvent")) {
		// event is now PullRequestEvent and is typeguarded.
	}
}
```
