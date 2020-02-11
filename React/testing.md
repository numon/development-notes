# Unit testing with enzyme

```jsx
import React from 'react';
import { mount } from 'enzyme';
import { Provider } from 'react-redux';
import { InfoBlock } from '../components';
import store from '..store';
import { infoMessage } from './store/reducers/Message';

describe('<InfoBox /> unit test', () => {
  let wrapper;
  beforeAll(() => {
    const getWrapper = () => mount(
      <Provider store={store}>
        <infoMessage />
      </Provider>,
    );
    wrapper = getWrapper();
  });

  it('Should render without errors', () => {
    expect(wrapper.length)
      .toBe(1);
  });

  it('Should see component parent node', () => {
    expect(wrapper.find('.InfoBox')
      .exists())
      .toEqual(true);
  });

  it('Should not see any message item when state is empty', () => {
    expect(wrapper.find('.infoItem')
      .exists())
      .toEqual(false);
  });

  it('Should see a message item when state is not empty', () => {
    store.dispatch(addInfoMessage({ type: 'error', message: 'Error message text' }));
    wrapper.update();
    expect(wrapper.find('.infoItem')
      .exists())
      .toEqual(true);
    expect(wrapper.find('.infoItem span')
      .text())
      .toEqual('error:Error message text');
  });

  it('Should not see any message when close message', () => {
    wrapper.find('button').simulate('click');
    expect(wrapper.find('.infoItem')
      .exists())
      .toEqual(false);
  });
});

```
