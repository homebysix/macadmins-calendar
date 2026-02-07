---
title: "About"
url: "/about/"
---

## Welcome!

Welcome to the Mac Admin community calendar! This site aims to provide an easy and dynamically updated resource for community members to reference major industry events such as conferences, regional meetups, and more.

## Event eligibility

Events that are a good fit for this calendar are:

- Broadly relevant to the Mac admin community, or
- Broadly relevant to specific subgroups of the community (e.g. geographic regions or customers of specific vendors)
- Offer high-quality technical or professionally relevant content
- Either in-person or virtual live events
- Either free or paid, but welcoming of all attendees

Events that will not be a good fit include:

- Sales pitches and non-technical product presentations
- Invite-only events
- Pre-recorded events

## Contributing

This site is open source and relies on community contributions to stay up to date. You can help by:

- **Adding new events**: Submit a pull request with new or recently-announced event details
- **Updating existing events**: Correct dates, locations, or other details
- **Improving the site**: Suggest new features or report bugs

### Data Format

Data for all events is located in the [data/events.yaml file on GitHub](https://github.com/homebysix/macadmins-calendar/blob/main/data/events.yaml).

Events are stored in YAML format with the following structure:

```yaml
- name: "Conference Name"
  full_name: "Longer More Descriptive Conference Name"  # optional
  start_date: "2025-07-15"
  end_date: "2025-07-18"
  location: "City, State/Province, Country"
  website: "https://example.com"
  type: "conference"
  videos: "https://youtube.com/channel"  # optional
  language: "en"                         # optional
```

## Questions or Suggestions?

Open an issue on [GitHub](https://github.com/homebysix/macadmins-calendar) or reach out to me through any of the channels mentioned above.
