# react-datepicker

An accessible, internationalizable, React datepicker.

## Installation

```Bash
yarn add @reecelucas/react-datepicker
```

## Example Usage

### Basic

```jsx
<DatePicker onSelect={date => console.log(date)}>
  <DatePickerInput />

  <DatePickerCalendar>
    <DatePickerMonth />
    <DatePickerButton updateMonth={({ prev }) => prev()}>
      Prev Month
    </DatePickerButton>
    <DatePickerButton updateMonth={({ next }) => next()}>
      Next Month
    </DatePickerButton>
    <DatePickerTable />
  </DatePickerCalendar>
</DatePicker>
```

### Initial Date

```jsx
<DatePicker
  initialDate={new Date(2020, 10, 10)}
  onSelect={date => console.log(date)}
>
  {/* ... */}
</DatePicker>
```

### Min Date

```jsx
<DatePicker
  minDate={new Date(2020, 0, 1)}
  onSelect={date => console.log(date)}
>
  {/* ... */}
</DatePicker>
```

### Max Date

```jsx
<DatePicker
  maxDate={new Date(2020, 0, 1)}
  onSelect={date => console.log(date)}
>
  {/* ... */}
</DatePicker>
```

### Date Range

```jsx
<DatePicker
  minDate={new Date(Date.now())}
  maxDate={new Date(2020, 0, 1)}
  onSelect={date => console.log(date)}
>
  {/* ... */}
</DatePicker>
```

### Exclude Dates

```jsx
<DatePicker
  excludeDates={[new Date(2019, 6, 1), new Date(2019, 6, 2)]}
  onSelect={date => console.log(date)}
>
  {/* ... */}
</DatePicker>
```

### Include Dates

```jsx
<DatePicker
  includeDates={[new Date(2019, 6, 1), new Date(2019, 6, 2)]}
  onSelect={date => console.log(date)}
>
  {/* ... */}
</DatePicker>
```

### Non-English Locale

Import the required date-fns [`locale`](https://date-fns.org/v2.0.0-alpha.37/docs/I18n#supported-languages)
and make sure to render a custom aria label for each day, using the `renderDayLabel` prop.

```jsx
import { format } from 'date-fns';
import locale from 'date-fns/locale/fr';

<DatePicker
  locale={locale}
  onSelect={date => console.log(date)}
>
  {/* ... */}
  <DatePickerCalendar>
    {/* ... */}
    <DatePickerTable
      renderDayLabel={({ date, isSelected, isSelectable }) => {
        const status = isSelected ? 'Sélectionné. ' : `${isSelectable ? 'Disponible. ' : 'Indisponible. '}`;
        return `${status}${format(date, 'eeee, do MMMM yyyy', { locale })}.`;
      }}
    />
  </DatePickerCalendar>
</DatePicker>
```

### Custom Month Format

Pass a valid date-fns [`format`](https://date-fns.org/v1.30.1/docs/format) string.

```jsx
<DatePicker onSelect={date => console.log(date)}>
  <DatePickerInput />

  <DatePickerCalendar>
    <DatePickerMonth dateFormat={'MMM, yyyy'} />
    {/* ... */}
  </DatePickerCalendar>
</DatePicker>
```

### Render Day Content

```jsx
import { getDate, isWeekend } from 'date-fns';

<DatePicker onSelect={date => console.log(date)}>
  {/* ... */}
  <DatePickerCalendar>
    {/* ... */}
    <DatePickerTable
      renderDayContent={date => (
        <span style={{ background: isWeekend(date) ? 'pink' : 'transparent' }}>
          {getDate(date)}
        </span>
      )}
    />
  </DatePickerCalendar>
</DatePicker>
```

### Custom Input Date Format

Pass a valid date-fns [`format`](https://date-fns.org/v1.30.1/docs/format) string.

```jsx
<DatePicker onSelect={date => console.log(date)}>
  <DatePickerInput dateFormat={'MM/dd/yyyy'} />
  {/* ... */}
</DatePicker>
```

### Custom Screen Reader Message

The `DatePickerInput` includes an `aria-describedby` attribute that references
a visually hidden aria message (for use by screen readers). The default message is:

```jsx
<>
  <p>
    Press the down arrow key to interact with the calendar and select a date.
    The following keyboard shortcuts can be used to change dates.
  </p>
  <ul>
    <li>Enter Key: select the date in focus.</li>
    <li>
      Right and left arrow keys: Move backward (left) and forward (right) by
      one day.
    </li>
    <li>
      Up and down arrow keys: Move backward (up) and forward (down) by one
      week.
    </li>
    <li>Page up and page down keys: Switch months.</li>
    <li>Home and end keys: go to the first or last day of a week.</li>
    <li>Escape key: Return to the date input field.</li>
  </ul>
</>
```

But you can render a custom message (E.g. written in another language if you're
passing a [`locale`](#non-english-locale)) by passing a render function...

```jsx
const renderScreenReaderMsg = () => (
  <p>
    I'm a custom screen reader message. I should describe how to interact with
    the date picker, playing special attention to the keyboard shortcuts that
    are available. This message won't be visible in the UI.
  </p>
);

<DatePicker onSelect={date => console.log(date)}>
  <DatePickerInput screenReaderMessage={renderScreenReaderMsg} />
  {/* ... */}
</DatePicker>
```

...Or by passing a JSX element

```jsx
<DatePicker onSelect={date => console.log(date)}>
  <DatePickerInput
    screenReaderMessage={
      <p>
        I'm a custom screen reader message. I should describe how to interact with
        the date picker, playing special attention to the keyboard shortcuts that
        are available. This message won't be visible in the UI.
      </p>
    }
  />
  {/* ... */}
</DatePicker>
```

## LICENSE

[MIT](./LICENSE)