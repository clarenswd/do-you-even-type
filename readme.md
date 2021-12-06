# Do you even type...Script?

My own very opinionated cheatsheet. _Surely there might be better ways, but then send me the link so I can learn 🤷‍♂️_


# React functional components

```tsx
export type ListProps = {
  //...
  filter?: string;
  //...
};

const List: React.FC<ListProps> = ({filter }: ListProps) => {
  if (R.isNil(filter)) {
    return null;
  }
  return <>SOME STUFF</>
}

export default List;

```

# Arrow functions 

_Probably this section name is not the only one._

```tsx
export type SasToken = {
    request?: string;
}

export type BlockClient = {
    //...
}

export const getBlockBlobClient = (request: SasToken): SasToken => {
    /// .... something with request
    return {name : "something "} as BlockClient
};

```

# Hooks 

## Type me the useState 

```tsx
... 
const [selectedActivity, setSelectedActivity] = useState<number>(0);

...

//and if there is a custom hooks

import {Dispatch, SetStateAction, useContext, useState} from 'react';
...
type StateSelectedActivity =  {
  selectedActivity: number;
  setSelectedActivity:  Dispatch<SetStateAction<number>>;
}
...

export default function useActivities(): [SecureRecord, ActivityTypeCount, StateSelectedActivity]  {
    ...
    return [... , {selectedActivity, setSelectedActivity}]
}


```

## Custom hooks

So you want to do the following:

```tsx
const [a, b ] = useCustomVars();
```

But Typescript lint is complaining? 
Add the return type in the hook function signature.

```tsx
...
export default function useActivities(): [SecureRecord, ActivityTypeCount] {
    ...
    return [
        {
            applicationState: record.applicationState,
            activities: record.activities,
        } as SecureRecord,
        activityTypeCount
    ];
}

```

## Typing props
You want to add a children functional component as a prop? There you go.

```

export interface ContainerProps extends ParentContainerProps {
    ...
    extraComponent?: React.FC<{className: string}>;
    ...
}

```



## Typing Ramda composed functions

So you created THE function. And the linter is ... complaining.
```ts

const ellipsis = R.pipe(R.slice(0, 200), R.append('...'), R.join(''));

...
// This is how I go around it, it's a hack
ellipsis((subText as unknown) as readonly unknown[])
``` 