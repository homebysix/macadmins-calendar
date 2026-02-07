# Mac Admin Conferences Calendar

A Hugo-powered static website for tracking Mac Admin conferences, meetups, and events worldwide. This site aims to provide an easy and dynamically updated resource for community members to reference major industry events.

## Development

Requires [Hugo](https://gohugo.io/installation/) (v0.100.0 or later).

1. Clone the repository:
   ```bash
   git clone https://github.com/homebysix/macadmins-calendar.git
   cd macadmins-calendar
   ```

2. Start the development server:
   ```bash
   hugo server -D
   ```

3. Open your browser to `http://localhost:1313`

## Contributing

Events are stored in `data/events.yaml`. To add a new event, please ensure it meets our event eligibility criteria below.

### Event Eligibility

Events that are a good fit for this calendar:

- Broadly relevant to the Mac admin community, or relevant to specific subgroups (e.g. geographic regions or customers of specific vendors)
- Offer high-quality technical or professionally relevant content
- Either in-person or virtual live events
- Either free or paid, but welcoming of all attendees

Events that will not be a good fit include:

- Sales pitches and non-technical product presentations
- Invite-only events
- Pre-recorded events

### Adding Events

1. Fork the repository
2. Edit `data/events.yaml`
3. Add your event using this format:

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

4. Submit a pull request

### Event Fields

- **name**: Conference/event name (required)
- **full_name**: Longer, more descriptive conference name (optional)
- **start_date**: Start date in YYYY-MM-DD format (required)
- **end_date**: End date in YYYY-MM-DD format, same as start_date for single-day events (required)
- **location**: City, State/Province, Country (required)
- **website**: Official website URL (required)
- **type**: Event type (`conference`, `meetup`, `workshop`, `webinar`) (required)
- **videos**: Video archive/YouTube channel URL (optional)
- **archive**: Archive/documentation URL (optional)
- **language**: Primary language code if not English, e.g. "en", "de", "fr" (optional)

**Note**: Event status (upcoming/past) is calculated automatically based on dates.

## Deployment

This site supports automated deployment with GitHub Pages, including daily rebuilds to automatically update event status (past/upcoming).

## License

Copyright 2026 Elliot Jordan

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
